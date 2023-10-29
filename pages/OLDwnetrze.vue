<template>
    <main>
		<div id="name"></div>
    </main>
  </template>
  <script setup>
  import gsap from "gsap";
  import * as THREE from "three";
  import { MapControls } from 'three/addons/controls/MapControls.js';
  import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";




var scene = new THREE.Scene();
    scene.background = new THREE.Color( '#fff' );
    
	scene.fog = new THREE.FogExp2( 0xcccccc, 0.02 );

var camera = new THREE.PerspectiveCamera( 30, innerWidth/innerHeight );
    camera.position.set( 4, 3, -7 );
    camera.lookAt( scene.position );

var renderer = new THREE.WebGLRenderer( {antialias: true} );
    renderer.setSize( innerWidth, innerHeight );
    document.body.appendChild( renderer.domElement );
			
window.addEventListener( "resize", (event) => {
    camera.aspect = innerWidth/innerHeight;
    camera.updateProjectionMatrix( );
    renderer.setSize( innerWidth, innerHeight );
});

const controls = new MapControls( camera, renderer.domElement );
  controls.enableDamping = true;
  controls.screenSpacePanning = false
  controls.autoRotate = false
  controls.mouseButtons = {
	LEFT: THREE.MOUSE.ROTATE,
	MIDDLE: THREE.MOUSE.DOLLY,
	RIGHT: THREE.MOUSE.PAN
}

renderer.outputColorSpace  = THREE.LinearSRGBColorSpace;

  const light = new THREE.AmbientLight(0xffffff, 3);
  scene.add(light);
  const directionalLight = new THREE.DirectionalLight(0xffffff, 2);
  scene.add(directionalLight);
  directionalLight.position.set(5, 1, 5);

  const directionalLight2 = new THREE.DirectionalLight(0xffffff, 2);
  scene.add(directionalLight2);
  directionalLight2.position.set(0, 3, 5);



var model,
		collectibles = []; // all model children with names

    const url = "/models/obiektPLUS.glb"
var loader = new GLTFLoader();
		loader.load( url, gltf => {
				model = gltf.scene;
				collectibles = [];
        console.log(collectibles)

				model.traverse( child =>
				{
						if( child.name != '' )
							collectibles.push( child );
					
						if( child.isMesh )
						{
								child.material = child.material.clone();
								child.material.metalness = 0;
								child.material.emissive.set( 'crimson' );
								child.material.emissiveIntensity = 0;
                
						}
				} );
			
        gltf.scene.position.set(0, 0, -2);
        gltf.scene.rotation.set(0, 3.4, 0);
        gsap.from(gltf.scene.position, 1.6, { z: 10 });
        gsap.from(gltf.scene.rotation, 1.6, { y: 1 });
				scene.add( model );
		} );







var raycaster = new THREE.Raycaster(),
		pointer = new THREE.Vector2( Infinity, Infinity );




function onPointerMove( event )
{
		pointer.x = 2*event.clientX/innerWidth - 1;
		pointer.y = -2*event.clientY/innerHeight + 1;
}


window.addEventListener( 'pointerdown', onPointerMove );




function setEmissive( child, value )
{
		if( child.isMesh )
				child.material.emissiveIntensity = value;
}




function selectNothing( )
{
		model.traverse( child => setEmissive(child,0) );
}




function selectElement( element )
{
		element.traverse( child => setEmissive(child,0) );
    console.log(element.name)
	
        const poka = document.getElementById('name')
        // console.log(poka)
        const link = element.name
        const href = 'https://brygida-arch.vercel.app/' + link
        const klikaj = '<a target="_blank" href=\"' + href + '\">' + link + '</a>'
        // console.log(klikaj)
        poka.innerHTML = klikaj
        
}


function animationLoop( t )
{
		// if the model is loaded test for hovering
		if( model )
		{
				selectNothing( );
			
				raycaster.setFromCamera( pointer, camera );
			
				var intersects = raycaster.intersectObjects( collectibles );
				if( intersects.length )
						selectElement( intersects[0].object );
		}
    controls.update( );
		light.position.copy( camera.position );
    renderer.render( scene, camera );
}

renderer.setAnimationLoop( animationLoop );





onUnmounted(() => {
    const canvasToDelete = document.querySelector('canvas')
    document.body.removeChild(canvasToDelete);
    console.log("canvasToDelete")
    console.log(canvasToDelete)
    console.log("wymontowyje");
  });



  </script>
  <style>
  #name {
    width: 100vw;
    height: 20vh;
    background-color: transparent;
    color: #fff;
    display: block;
    z-index: 147;
    position: absolute;
    display: block;
    top: 15vh; left: 0;
    font-size: 3em;
}
  </style>
  