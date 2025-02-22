<script>
    import * as THREE from 'three';
    import { T, useTask } from '@threlte/core';
    import { RigidBody, Collider, useRigidBody, AutoColliders } from '@threlte/rapier';
    import { readable } from 'svelte/store';

    let matcapTexture = readable(new THREE.TextureLoader().load('/matcap.png'));  

    let {
        scale = 1
      } = $props();
  
    let r = THREE.MathUtils.randFloatSpread

     // Reference to the rigid body
    let rigidBody = $state()
    let vec = new THREE.Vector3()  
    // Apply impulse during each frame update
    useTask(( delta ) => {
       
       if(rigidBody) {
         // Limit the delta to prevent large jumps
       delta = Math.min(0.1, delta);
   
         //Apply impulse to the rigid body
         rigidBody.applyImpulse(
             vec
             .copy(rigidBody.translation())
             .normalize()
             .multiply({ x: -50 * delta * scale, y: -150 * delta * scale, z: -50 * delta * scale }),
         );
       }
     });
  </script>
 
<T.Group position={[r(20), r(20) - 25, r(20) - 10]}>
    <RigidBody    
        linearDamping={0.75}
        angularDamping={0.15}
        friction={0.2}        
        bind:rigidBody
        colliders={false}
    >
        <Collider shape="ball" args={[scale]}>
            <T.Mesh scale={[scale, scale, scale]} castShadow receiveShadow>
                <T.SphereGeometry args={[1, 64, 64]} />
                <!-- <T.MeshMatcapMaterial bind:matcap={$matcapTexture} /> -->
                <T.MeshPhysicalMaterial 
                  color="#E2DFD2"
                  roughness={1}
                  metalness={0.3}
                  clearcoat={1.0} 
                  clearcoatRoughness={0.1}
              />
            </T.Mesh>
        </Collider>
    </RigidBody>
</T.Group>