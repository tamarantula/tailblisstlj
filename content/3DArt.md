---
title: 3D Art
date: 2021-12-18T03:10:36.000Z
draft: false
language: en
description: My 3D Art
---
<script src="https://cdn.tailwindcss.com"></script>
<head>
<!--First 3D Art Piece-->
    <div class="relative w-screen flex" style="margin-left: calc(-50vw + 50%);">
<!--3D Art 1-->
        <canvas id="first-3Dart" class="block flex-shrink-0" width="1000px" height="750px"></canvas>
<!--Text Boxes UI (popout)-->
        <div class="flex-1 relative">
            <div class="absolute select-none pointer-events-none
                top-2 right-2
                sm:top-5 sm:right-5
                md:top-10 md:right-10
                lg:top-20 lg:right-20">
                <div id="first-container" class="absolute top-[20px] right-[200px]">
                <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 right-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
                    <div class="relative z-10 w-[225px] h-[120px] p-4 not-prose">
                        <p class="font-semibold text-4xl text-center">Title 1</p>
                        <p class="font-semibold text-2xl pt-2 p-0 m-0">Blah Blah Blah 1...</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</head>

<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.179.1/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.165.0/examples/jsm/"
  }
}
</script>

<script type="module">
//Importing
import * as THREE from 'three';
import {OrbitControls} from 'three/addons/controls/OrbitControls.js';
import {OBJLoader} from 'three/addons/loaders/OBJLoader.js';
import {MTLLoader} from 'three/addons/loaders/MTLLoader.js';

//Create a scene
const scene = new THREE.Scene();
scene.background = null; //makes it so there is no background, resulting in the 3.js default black screen

//get canvas element FIRST
const canvas = document.getElementById('first-3Dart');

//Define camera placement
const fov = 40;
const aspect = 1.5; //the canvas default
const near = 0.1;
const far = 100;
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);

//Orbit controls (spin around object)
const controls = new OrbitControls(camera, canvas);
controls.target.set(0, 5, 0);
controls.enableZoom = false;
controls.enablePan = false;
controls.update();

//Create lighting
//Defining (for both lights)
const color = 0xFFFFFF;
const intensity = 5;
//Ambient
const light = new THREE.AmbientLight(color, intensity);
//Adding to scene
scene.add(light);

//Create a Renderer
const renderer = new THREE.WebGLRenderer({canvas: canvas, alpha: true}); //alpha overwrite's 3.js fallback baclground (above code) to the transparent background
renderer.setSize(canvas.clientWidth, canvas.clientHeight); //uses my defined canvas size

let loadedMesh = null;

//First 3D Mesh
//Importing Texture
const mtlLoader = new MTLLoader();
const objLoader = new OBJLoader();
/*
mtlLoader.load('/3DObjects/NavSqr.mtl', (mtl) => {
  mtl.preload();
  objLoader.setMaterials(mtl);
  //Importing Mesh
  objLoader.load('/3DObjects/NavSqr.obj', (root) => {
    //Cemter the mesh
    const box = new THREE.Box3().setFromObject(root);
    const center = box.getCenter(new THREE.Vector3());
    const size = box.getSize(new THREE.Vector3());

    root.position.sub(center);
    scene.add(root);

    //Add this line to store it globally
    loadedMesh = root;

    //Position camera based on object size
    const maxDimension = Math.max(size.x, size.y, size.z);
    const distance = maxDimension * 2; //2x the object's size

    camera.position.set(0, distance * 1, distance);
    controls.target.set(0, 0, 0);
    controls.update();

    //Update controls target to the object center
    controls.target.copy(root.position);
    controls.update();
        
    // Render the scene once after the object is loaded and centered
    //renderer.render(scene, camera);
    animate();
  });
});

//Animation Loop (needed for orbit)
function animate() {
  if (loadedMesh) {
    const faceNumber = detectFaceFromCamera(loadedMesh, camera);
  }
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}
*/
</script>
