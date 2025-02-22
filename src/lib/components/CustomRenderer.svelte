<script lang="ts">
    import { onMount } from 'svelte'
    import { useThrelte, useTask } from '@threlte/core'
    import { N8AOPostPass } from 'n8ao'
    import * as THREE from 'three'
    import {
        EffectComposer,
        EffectPass,
        RenderPass,
        SMAAEffect,
        SMAAPreset
    } from 'postprocessing'

    const { size, scene, renderer, camera, renderStage, autoRender } = useThrelte()
    const composer = new EffectComposer(renderer)

    function setupEffectComposer(cam) {
        composer.removeAllPasses()
        composer.addPass(new RenderPass(scene, cam))

        const n8aopass = new N8AOPostPass(scene, cam, $size.width, $size.height)
        n8aopass.configuration.aoRadius = 20
        n8aopass.configuration.intensity = 2
        n8aopass.configuration.color.set('#a020f0')

        composer.addPass(n8aopass)
        composer.addPass(
            new EffectPass(
                cam,
                new SMAAEffect({
                    preset: SMAAPreset.HIGH
                })
            )
        )
    }

    onMount(() => {
        // Subscribe to camera changes
        const unsubCamera = camera.subscribe(value => {
            setupEffectComposer(value)
        })

        // Subscribe to size changes
        const unsubSize = size.subscribe(({ width, height }) => {
            composer.setSize(width, height)
        })

        // Turn off auto-render and restore on teardown
        const before = autoRender.current
        autoRender.set(false)

        return () => {
            unsubCamera()
            unsubSize()
            autoRender.set(before)
        }
    })

    useTask((delta) => {
        composer.render(delta)
    }, { stage: renderStage, autoInvalidate: false })
</script>