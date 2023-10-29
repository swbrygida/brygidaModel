<template>
    <main>
      <div id="loading"><p>Loading.. Ładuje model 3d..</p></div>
      <div id="loading-bar"></div>
    </main>
  </template>
  <script setup>
  import * as THREE from "three";
  import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";
  import { FirstPersonControls } from 'three/addons/controls/FirstPersonControls.js';
  
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  const scene = new THREE.Scene();
  const renderer = new THREE.WebGLRenderer({ alpha: true });
  renderer.setSize(window.innerWidth * 0.95, window.innerHeight * 0.9);
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
    gltf.scene.position.set(0, 0, 0);
    gltf.scene.rotation.set(0, -4, 0);
  });
  
  camera.position.z = 4;
  camera.position.x = 1;
  camera.position.y = 1;
  renderer.render(scene, camera);
  
const controls = new FirstPersonControls(camera, renderer.domElement)
controls.enabled = true
controls.mouseDragOn = false
controls.activeLook = true
controls.noFly = true;
controls.lookSpeed = 0.09
controls.movementSpeed = 0.4
controls.lookVertical = true
controls.constrainVertical = false
controls.verticalMin = Math.PI / 1.7
controls.verticalMax = Math.PI / 2.3
  
  function animate() {
    requestAnimationFrame(animate);
    controls.update(0.01);
    renderer.render(scene, camera);
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
  