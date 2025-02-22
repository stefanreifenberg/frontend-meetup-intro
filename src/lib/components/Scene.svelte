<script>
    import { T,useThrelte } from '@threlte/core';
    import { Grid, OrbitControls, Environment} from '@threlte/extras'
    import * as THREE from 'three';
    import { AutoColliders } from '@threlte/rapier'
    import Pointer from './Pointer.svelte';
    import Sphere from './Sphere.svelte';

    const { renderer } = useThrelte();

    // Configure tone mapping on the renderer
    renderer.toneMapping = THREE.AgXToneMapping;
    renderer.toneMappingExposure = 1.5;

    // Generate spheres
    const randomGaussian = (mean, stdDev) => {
    let u = 1 - Math.random();
    let v = 1 - Math.random();
    let z = Math.sqrt(-2.0 * Math.log(u)) * Math.cos(2.0 * Math.PI * v);
    return mean + z * stdDev;
};

const spheres = $state(
    Array.from({ length: 50 }, () => ({
        scale: Math.max(0.5, randomGaussian(1, 0.2)) // Mean 1, std dev 0.2, min 0.5
    }))
);
</script>
  
  <!-- Camera setup -->
<T.PerspectiveCamera
    makeDefault
    position={[0, 0, -20]}
    fov={32.5}
    oncreate={(ref) => {
        ref.lookAt(0, 1, 0)
    }}
    >    
</T.PerspectiveCamera>

<Environment url="adamsbridge.hdr" />

<!-- Lighting setup -->
<T.AmbientLight intensity={4} />
<T.SpotLight position={[20, 20, 25]} penumbra={1} angle={0.2} color="white" intensity={8} castShadow shadow-mapSize={[1024, 1024]} />
<T.DirectionalLight position={[0, 5, -4]} intensity={1} />
<T.DirectionalLight position={[0, -15, -0]} intensity={1} color="white" />

<!-- Render multiple spheres -->
{#each spheres as { scale }, i}
    <Sphere scale={scale} />
{/each}

<Pointer />

