---
title: Tam's Website
date: 2021-12-18T11:10:36+08:00
draft: false
language: en
description: My Games
---
<script src="https://cdn.tailwindcss.com"></script>
<head>
  <div class="relative my-4">
    <!--Title-->
    <div class="ml-[-700px] mb-[150px]">
      <svg width="650px" height="80px">
          <rect width="650px" height="80px" fill="black"></rect>
          <text class="font-semibold text-4xl" x="295" y="51" fill="white">Games I Have Made</text>
      </svg>
    </div>
    <div class="lg:mx-auto lg:max-w-7xl lg:items-start lg:px-8">
      <div class="absolute select-none pointer-events-none
        top-4 left-4
        sm:top-10 sm:left-10
        md:top-15 md:left-15
        lg:top-25 lg:left-25">
        <div id="container-for-ui-first" class="invisible duration-700">
          <p class="font-semibold text-4xl">Game 1</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 1...</p>
          </div>
        </div>
        <div id="container-for-ui-second" class="invisible duration-700">
        <p class="font-semibold text-4xl">Game 2</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 2...</p>
          </div>
        </div>
        <div id="container-for-ui-third" class="invisible duration-700">
        <p class="font-semibold text-4xl">Game 3</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 3...</p>
          </div>
        </div>
        <div id="container-for-ui-fourth" class="invisible duration-700">
        <p class="font-semibold text-4xl">Game 4</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 4...</p>
          </div>
        </div>
        <div id="container-for-ui-fifth" class="invisible duration-700">
        <p class="font-semibold text-4xl">Game 5</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 5...</p>
          </div>
        </div>
        <div id="container-for-ui-sixth" class="invisible duration-700">
        <p class="font-semibold text-4xl">Game 6</p>
          <div class="flex justify-items-center">
            <p class="text-center font-semibold text-2xl pt-2">Blah Blah Blah 6...</p>
          </div>
        </div>
      </div>
      <canvas id="sqr" class="mx-auto block" width="1260" height="870"></canvas>
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

//Get canvas element FIRST
const canvas = document.getElementById('sqr');
//Get My Games Info UI
const firstgame = document.getElementById("container-for-ui-first");
const secondgame = document.getElementById("container-for-ui-second");
const thirdgame = document.getElementById("container-for-ui-third");
const fourthgame = document.getElementById("container-for-ui-fourth");
const fifthgame = document.getElementById("container-for-ui-fifth");
const sixthgame = document.getElementById("container-for-ui-sixth");

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
controls.addEventListener('start', function(){   //for removing image
  firstgame.replace("visible", "invisible");
  secondgame.replace("visible", "invisible");
  thirdgame.replace("visible", "invisible");
  fourthgame.replace("visible", "invisible");
  fifthgame.replace("visible", "invisible");
  sixthgame.replace("visible", "invisible");
})
controls.update();

//Making previous face 0
let previousFace = null;

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

// Add this at the top with your other variables
let loadedMesh = null;

//Cube 3D Mesh
//Importing Texture
const mtlLoader = new MTLLoader();
const objLoader = new OBJLoader();
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

    /*
    //Debug code:
    console.log("Loaded object type:", root.type);
    console.log("Loaded object:", root);
    console.log("Children:", root.children);
    root.traverse((child) => {
        console.log("Child type:", child.type, "Is Mesh:", child.isMesh);
    });*/

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

let lastFaceIndex = null;

//Face detection functions
function detectFaceFromCamera(mesh, camera) {
  const raycaster = new THREE.Raycaster();
  const centscr = new THREE.Vector2(0, 0); //Center of screen

  //Cast ray from camera through center of screen
  raycaster.setFromCamera(centscr, camera);

  //Get intersections with the mesh
  const intersections = raycaster.intersectObjects(scene.children, true);

  if (intersections.length > 0) {
    const faceIndex = intersections[0].faceIndex;
    
    //Only log if face changed - to not keep console overcrowded
    /*
    if (faceIndex !== lastFaceIndex) {
      console.log(`Camera looking at face: ${faceIndex}`);
      lastFaceIndex = faceIndex;
    }*/
    return faceIndex;
  }
  lastFaceIndex = null;
  return null; //no intersection
}

//Animation Loop (needed for orbit)
function animate() {
  if (loadedMesh) {
    const faceNumber = detectFaceFromCamera(loadedMesh, camera);
  }
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);
}

//Initializing stuff
const raycaster = new THREE.Raycaster(); //Creating Raycaster
document.addEventListener('dblclick', dblclick); //Listens for double mouse click
//const centface = new THREE.Vector2(0, 0); //Center of screen - for raycaster

//Clicking on Face event
function dblclick (event) {
  console.log("Double click detected!");
  console.log("Event clientX:", event.clientX, "clientY:", event.clientY);

  //Get Canvas bounding box
  const rect = canvas.getBoundingClientRect();
  console.log("Canvas rect:", rect);

  //Calculate pointer position
  const coords = new THREE.Vector2(
      ((event.clientX - rect.left) / rect.width) * 2 - 1,
      -((event.clientY - rect.top) / rect.height) * 2 - 1,
  ); 

  //Return
  raycaster.setFromCamera(coords, camera);
  
  //Calculate objects intersecting the picking ray - Raycast against the group AND its children (recursive = true)
  const intersections = raycaster.intersectObjects([loadedMesh], true); 
  
  if (intersections.length > 0) {
    //Accessing the faceIndex values
    const faceIndexValue = intersections[0].faceIndex;
    const previousFace = faceIndexValue; 

    const baseURL = "{{ .Site.BaseURL }}";
    //Main: Redirection
    //console.log(`Clicking on face: ${faceIndexValue}`);
    //For "1" face
    if (faceIndexValue == 191) {
      firstgame.classList.replace("invisible", "visible");
      if (previousFace == 191) {
        window.location.href = baseURL + "/devlogs/game-1/";
      }
    }
    //For "2" face 
    if (faceIndexValue == 49) {
      secondgame.classList.replace("invisible", "visible");
      if (previousFace == 49) {
        window.location.href = baseURL + "/devlogs/game-2/";
      }
    }
    //For "3" face 
    if (faceIndexValue == 26) {
      thirdgame.classList.replace("invisible", "visible");
      if (previousFace == 26) {
        window.location.href = baseURL + "/devlogs/game-3/";
      }
    }
    //For "4" face 
    if (faceIndexValue == 159) {
      fourthgame.classList.replace("invisible", "visible");
      if (previousFace == 159) {
        window.location.href = baseURL + "/devlogs/game-4/";
      }
    }
    //For "5" face 
    if (faceIndexValue == 147) {
      fifthgame.classList.replace("invisible", "visible");
      if (previousFace == 147) {
        window.location.href = baseURL + "/devlogs/game-5/";
      }
    }
    //For "6" face 
    if (faceIndexValue == 191) {
      sixthgame.classList.replace("invisible", "visible");
      if (previousFace == 191) {
        window.location.href = baseURL + "/devlogs/game-6/";
      }
    }
  }
  else {
    console.log("No intersections found with either method!!");
  }
}
</script>