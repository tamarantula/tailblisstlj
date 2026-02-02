---
title: Tam's Website
date: 2021-12-18T11:10:36+08:00
draft: false
language: en
description: My Games
---
<script src="https://cdn.tailwindcss.com"></script>
<head>
  <!--Title-->
  <div class="relative mb-[150px] w-screen" style="margin-left: calc(-50vw + 50%);">
    <svg width="650px" height="80px" class="drop-shadow-3xl">
        <rect width="650px" height="80px" fill="black"></rect>
        <text class="font-semibold text-4xl" x="295" y="51" fill="white">Games I Have Made</text>
    </svg>
  </div>
  <!--Center Container-->
  <div class="relative w-screen flex" style="margin-left: calc(-50vw + 50%);">
    <!--Text Boxes UI (popout)-->
    <div class="flex-1 relative">
      <div class="absolute select-none pointer-events-none
        top-2 left-2
        sm:top-5 sm:left-5
        md:top-10 md:left-10
        lg:top-20 lg:left-20">
        <div id="container-for-ui-first" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-[120px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 1</p>
            <p class="font-semibold text-2xl pt-2 p-0 m-0">Blah Blah Blah 1...</p>
          </div>
        </div>
        <div id="container-for-ui-second" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-[120px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 2</p>
            <p class="font-semibold text-2xl pt-2">Blah Blah Blah 2...</p>
          </div>
        </div>
        <div id="container-for-ui-third" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-[120px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 3</p>
            <p class="font-semibold text-2xl pt-2">Blah Blah Blah 3...</p>
          </div>
        </div>
        <div id="container-for-ui-fourth" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-"120px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 4</p>
            <p class="font-semibold text-2xl pt-2">Blah Blah Blah 4...</p>
          </div>
        </div>
        <div id="container-for-ui-fifth" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-"120px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 5</p>
            <p class="font-semibold text-2xl pt-2">Blah Blah Blah 5...</p>
          </div>
        </div>
        <div id="container-for-ui-sixth" class="invisible absolute top-0 left-0 duration-700">
          <svg width="225px" height="120px" class="drop-shadow-3xl absolute top-0 left-0"><rect width="225px" height="120px" fill="#F4F4F9"></rect></svg>
          <div class="relative z-10 w-[225px] h-[335px] p-4 not-prose">
            <p class="font-semibold text-4xl text-center">Game 6</p>
            <p class="font-semibold text-2xl pt-2">Blah Blah Blah 6...</p>
          </div>
        </div>
      </div>
    </div>
    <!--3D Cube-->
    <canvas id="sqr" class="block flex-shrink-0" width="1260" height="870"></canvas>
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
  firstgame.classList.replace("visible", "invisible");
  secondgame.classList.replace("visible", "invisible");
  thirdgame.classList.replace("visible", "invisible");
  fourthgame.classList.replace("visible", "invisible");
  fifthgame.classList.replace("visible", "invisible");
  sixthgame.classList.replace("visible", "invisible");
})
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

    //Add wireframe to visualize triangle edges
    /*
    root.traverse((child) => {
      if (child.isMesh) {
        const wireframeGeometry = new THREE.WireframeGeometry(child.geometry);
        const wireframeMaterial = new THREE.LineBasicMaterial({ color: 0x00ff00, linewidth: 2 });
        const wireframe = new THREE.LineSegments(wireframeGeometry, wireframeMaterial);
        child.add(wireframe);
      }
    });
    */

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

//This is for face cube logic at bottom of code
let previousFace = null;

//This is for the code below
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
canvas.addEventListener('dblclick', dblclick); //Listens for double mouse click
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
      -(((event.clientY - rect.top) / rect.height) * 2 - 1),
  ); 

  //Return
  raycaster.setFromCamera(coords, camera);
  
  //Calculate objects intersecting the picking ray - Raycast against the group AND its children (recursive = true)
  const intersections = raycaster.intersectObjects(scene.children, true); //[loadedMesh]
  
  if (intersections.length > 0) {
    //Accessing the faceIndex values
    const faceIndexValue = intersections[0].faceIndex; 

    const baseURL = "{{ .Site.BaseURL }}";
    //Main: Redirection
    console.log(`Clicking on face: ${faceIndexValue}`);
    //For "1" face
    if ([8, 9].includes(faceIndexValue)) {
      if ([8, 9].includes(previousFace)) { //second click
        window.location.href = baseURL + "/game-1/";
      }
      else { //first click
        firstgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
    }
    //For "2" face 
    else if ([48, 49].includes(faceIndexValue)) {
      if ([48, 49].includes(previousFace)) {
        window.location.href = baseURL + "/game-2/";
      }
      else {
        secondgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
    }
    //For "3" face 
    else if ([28, 29].includes(faceIndexValue)) {
      if ([28, 29].includes(previousFace)) {
        window.location.href = baseURL + "/game-3/";
      }
      else {
        thirdgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
    }
    //For "4" face 
    else if ([18, 19].includes(faceIndexValue)) {
      if ([18, 19].includes(previousFace)) {
        window.location.href = baseURL + "/game-4/";
      }
      else {
        fourthgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
    }
    //For "5" face 
    else if ([58, 59].includes(faceIndexValue)) {
      if ([58, 59].includes(previousFace)) {
        window.location.href = baseURL + "/devlogs/game-5/";
      }
      else {
        fifthgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
    }
    //For "6" face 
    else if ([30, 31].includes(faceIndexValue)) {
      if ([30, 31].includes(previousFace)) {
        window.location.href = baseURL + "/devlogs/game-6/";
      }
      else {
        sixthgame.classList.replace("invisible", "visible");
        previousFace = faceIndexValue;
      }
      /*
          if (faceIndexValue == [8, 9]) {
      if (previousFace == [8, 9]) { //second click
        window.location.href = baseURL + "/game-1/";
      }
      else { //first click
        firstgame.classList.replace("invisible", "visible");
        previousFace = [8, 9];
      }
    }
    //For "2" face 
    else if (faceIndexValue == [48, 49]) {
      if (previousFace == [48, 49]) {
        window.location.href = baseURL + "/game-2/";
      }
      else {
        secondgame.classList.replace("invisible", "visible");
        previousFace = [48, 49];
      }
    }
    //For "3" face 
    else if (faceIndexValue == [28, 29]) {
      if (previousFace == [28, 29]) {
        window.location.href = baseURL + "/game-3/";
      }
      else {
        thirdgame.classList.replace("invisible", "visible");
        previousFace = [28, 29];
      }
    }
    //For "4" face 
    else if (faceIndexValue == [18, 19]) {
      if (previousFace == [18, 19]) {
        window.location.href = baseURL + "/game-4/";
      }
      else {
        fourthgame.classList.replace("invisible", "visible");
        previousFace = [18, 19];
      }
    }
    //For "5" face 
    else if (faceIndexValue == [58, 59]) {
      if (previousFace == [58, 59]) {
        window.location.href = baseURL + "/devlogs/game-5/";
      }
      else {
        fifthgame.classList.replace("invisible", "visible");
        previousFace = [58, 59];
      }
    }
    //For "6" face 
    else if (faceIndexValue == [30, 31]) {
      if (previousFace == [30, 31]) {
        window.location.href = baseURL + "/devlogs/game-6/";
      }
      else {
        sixthgame.classList.replace("invisible", "visible");
        previousFace = [30, 31];
      }
      */
    }
    else {
      previousFace = null; //resets if clicking a different face
    }
  }
  else {
    console.log("No intersections found with either method!!");
    previousFace = null;
  }
}
</script>