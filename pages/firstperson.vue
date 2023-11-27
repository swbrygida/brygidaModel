<template>
    <main>
      <div id="loading"><p>Loading.. Ładuje model 3d..</p></div>
      <div id="loading-bar"></div>
    </main>
  </template>
  <script setup>
  import * as THREE from "three";
  import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";  
  import { PointerLockControls } from 'three/addons/controls/PointerLockControls.js';
  
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  const scene = new THREE.Scene();
  const renderer = new THREE.WebGLRenderer({ alpha: true });
  renderer.setSize(window.innerWidth * 1, window.innerHeight * 1);
  document.body.appendChild(renderer.domElement);
  
  const light = new THREE.AmbientLight(0xffffff, 2);
  scene.add(light);
  const directionalLight = new THREE.DirectionalLight(0xffffff, 3);
  scene.add(directionalLight);
  directionalLight.position.set(5, 1, 5);
  
  const loadingMenager = new THREE.LoadingManager(
// loaded 
() => {
  window.setTimeout(() => {
  const loadingNapis = document.getElementById('loading')
  loadingNapis.style.display = 'none'
  const loadingElement = document.getElementById('loading-bar')
  loadingElement.style.transformOrigin = 'top right'
  loadingElement.style.transform = 'scaleX(0)'
  }, 500)
},
// progress
(itemUrl, itemsLoaded, itemsTotal) => {
  const loadingElement = document.getElementById('loading-bar')
  const progress = itemsLoaded / itemsTotal
  loadingElement.style.transform = 'scaleX(' + progress + ')'
}
);


  const gltfLoader = new GLTFLoader(loadingMenager);
  const url = "/models/obiektPLUS.glb"
  gltfLoader.load(url, (gltf) => {
    console.log(gltf.scene);
    scene.add(gltf.scene);
    gltf.scene.position.set(0, 9.4, 0);
    gltf.scene.rotation.set(0, 1.6, 0);
  });
  
  camera.position.z = 4;
  camera.position.x = 0;
  camera.position.y = 0;
  renderer.render(scene, camera);
  
  let controls = new PointerLockControls( camera, document.body );

  controls.isLocked = true

  scene.add( controls.getObject() );
  

  let raycaster;
  raycaster = new THREE.Raycaster( new THREE.Vector3(), new THREE.Vector3( 0, - 1, 0 ), 0, 10 );

let moveForward = false;
let moveBackward = false;
let moveLeft = false;
let moveRight = false;
let canJump = false;

let prevTime = performance.now();
const velocity = new THREE.Vector3();
const direction = new THREE.Vector3();



  const onKeyDown = function ( event ) {

switch ( event.code ) {

  case 'ArrowUp':
  case 'KeyW':
    moveForward = true;
    break;

  case 'ArrowLeft':
  case 'KeyA':
    moveLeft = true;
    break;

  case 'ArrowDown':
  case 'KeyS':
    moveBackward = true;
    break;

  case 'ArrowRight':
  case 'KeyD':
    moveRight = true;
    break;

  case 'Space':
    if ( canJump === true ) velocity.y += 35;
    canJump = false;
    break;

}

};

const onKeyUp = function ( event ) {

switch ( event.code ) {

  case 'ArrowUp':
  case 'KeyW':
    moveForward = false;
    break;

  case 'ArrowLeft':
  case 'KeyA':
    moveLeft = false;
    break;

  case 'ArrowDown':
  case 'KeyS':
    moveBackward = false;
    break;

  case 'ArrowRight':
  case 'KeyD':
    moveRight = false;
    break;

}

};

document.addEventListener( 'keydown', onKeyDown );
document.addEventListener( 'keyup', onKeyUp );



  function animate() {
    requestAnimationFrame( animate );

const time = performance.now();

if ( controls.isLocked === true ) {

  raycaster.ray.origin.copy( controls.getObject().position );
  raycaster.ray.origin.y -= 10;

  const intersections = raycaster.intersectObjects( scene );

  const onObject = intersections.length > 0;

  const delta = ( time - prevTime ) / 1000;

  velocity.x -= velocity.x * 6.0 * delta;
  velocity.z -= velocity.z * 6.0 * delta;

  velocity.y -= 9.8 * 100.0 * delta; // 100.0 = mass

  direction.z = Number( moveForward ) - Number( moveBackward );
  direction.x = Number( moveRight ) - Number( moveLeft );
  direction.normalize(); // this ensures consistent movements in all directions

  if ( moveForward || moveBackward ) velocity.z -= direction.z * 6.0 * delta;
  if ( moveLeft || moveRight ) velocity.x -= direction.x * 6.0 * delta;

  if ( onObject === true ) {

    velocity.y = Math.max( 0, velocity.y );
    canJump = true;

  }

  controls.moveRight( - velocity.x * delta );
  controls.moveForward( - velocity.z * delta );

  controls.getObject().position.y += ( velocity.y * delta ); // new behavior

  if ( controls.getObject().position.y < 10 ) {

    velocity.y = 0;
    controls.getObject().position.y = 10;

    canJump = true;

  }

}

prevTime = time;

renderer.render( scene, camera );
  }
  animate();
  
  onUnmounted(() => {
    const canvasToDelete = document.querySelector('canvas')
    document.body.removeChild(canvasToDelete);
    console.log("canvasToDelete")
    console.log(canvasToDelete)
    console.log("wymontowyje");
  });
  </script>
  <style></style>
  