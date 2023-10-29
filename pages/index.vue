<template>
    <main>
      <div id="loading-bar-index"></div>

    </main>
  </template>
  <script setup>
  import gsap from "gsap";
  import * as THREE from "three";
  import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";
  import { MapControls } from 'three/addons/controls/MapControls.js';

  
  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  const scene = new THREE.Scene();
  scene.background = new THREE.Color( 0xcccccc );
	scene.fog = new THREE.FogExp2( 0xcccccc, 0.2 );


  const renderer = new THREE.WebGLRenderer({ alpha: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);
  
  const light = new THREE.AmbientLight(0xffffff, 0.5);
  scene.add(light);
  const directionalLight = new THREE.DirectionalLight(0xffffff, 3);
  scene.add(directionalLight);
  directionalLight.position.set(-1, -1, 2);
  

  const loadingMenager = new THREE.LoadingManager(
// loaded 
() => {
  window.setTimeout(() => {
  const loadingElement = document.getElementById('loading-bar-index')
  loadingElement.style.transformOrigin = 'top right'
  loadingElement.style.transform = 'scaleX(0)'
  }, 500)
},
// progress
(itemUrl, itemsLoaded, itemsTotal) => {
  const loadingElement = document.getElementById('loading-bar-index')
  const progress = itemsLoaded / itemsTotal
  loadingElement.style.transform = 'scaleX(' + progress + ')'
}
);


  const gltfLoader = new GLTFLoader(loadingMenager);
  const url = "/models/obiektZ.glb";
  gltfLoader.load(url, (gltf) => {
    console.log(gltf.scene);
    gltf.scene.position.set(0, -2.2,-1);
    gltf.scene.rotation.set(0, 1.2, 0);
    gsap.from(gltf.scene.position, 1.6, { z: -7 });
    gsap.from(gltf.scene.rotation, 1.6, { y: -2 });
    scene.add(gltf.scene);
  });
  



  camera.position.z = 6;
  camera.position.x = 1;
  camera.position.y = 2;
  renderer.render(scene, camera);
  
  const controls = new MapControls( camera, renderer.domElement );
  controls.enableDamping = true;
  controls.screenSpacePanning = false
  controls.autoRotate = true
  controls.autoRotateSpeed = 0.05
  controls.mouseButtons = {
	LEFT: THREE.MOUSE.ROTATE,
	MIDDLE: THREE.MOUSE.DOLLY,
	RIGHT: THREE.MOUSE.PAN
}


  
  function animate() {
    requestAnimationFrame(animate);
    controls.update();
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
  <style>
  #loading-bar-index {
  position: absolute;
  top: 50%; left: 0;
  height: 3px;
  width: 100%;;
  background-color: #f4f4f4;
  transform: scaleX(0);
  transform-origin: top left;
  transition: transform 0.3s;

}
  </style>
  