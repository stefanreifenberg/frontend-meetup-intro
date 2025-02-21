<script>
    import * as THREE from 'three';
    import { T, useTask } from '@threlte/core';
    import { RigidBody, Collider } from '@threlte/rapier';
    import { interactivity, useInteractivity } from '@threlte/extras';
  
    // Enable interactivity globally
    interactivity();
    
    // Access pointer data from interactivity hook
    const { pointer } = useInteractivity();
  
    // Create a reactive reference for the RigidBody
    let rigidBody = $state()
    let vec = new THREE.Vector3()
    let positionArray = $state()
  
    // Update position on each frame using useTask
    useTask(() => {
        if(rigidBody) {
            vec.lerp(new THREE.Vector3(-$pointer.x * 5, $pointer.y * 5, 0), 1);
            rigidBody.setNextKinematicTranslation(vec);
            positionArray = vec.toArray();
        }   
    });
  </script>
  
  <!-- Render the RigidBody and Collider -->
  <RigidBody
    bind:rigidBody
    type="kinematicPosition"
    colliders={false}
  >
    <Collider shape="ball" args={[1]} />
  </RigidBody>
