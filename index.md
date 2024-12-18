# Multi-Scene Setup in `multi` Folder

The `multi` folder contains a multi-scene setup for our Babylon.js project. This setup allows you to switch between different scenes within the same application. Below is a brief explanation of how it works:

## Folder Structure

The `multi` folder is organized as follows:

multi/src/scene1/scene2/scene4/gui/index.ts main.css

Each scene is implemented in its own folder under `src/`. For example:
- `scene1/` contains the code for the first scene.
- `scene2/` contains the code for the second scene.
- `scene3/` contains the code for the third scene.
- `scene4/` contains the code for the fourth scene.
- `gui/` contains the code for the GUI scene.

To make things work in the end I removed scene3 as it wouldn't work in the multi scene but was fine in its own element.

### Main Entry Point

The main entry point for the application is `index.ts` in the `multi` folder. This file initializes the Babylon.js engine and sets up the scenes.

```ts
import { Engine } from "@babylonjs/core";
import createScene1 from "./scene1/src/createStartScene";
import createScene2 from "./scene2/src/createStartScene";
import createScene3 from "./scene3/src/createStartScene";
import createScene4 from "./scene4/gui04/src/gameScene";
import menuScene from "./gui/guiScene";
import "./main.css";

const CanvasName = "renderCanvas";

let canvas = document.createElement("canvas");
canvas.id = CanvasName;

canvas.classList.add("background-canvas");
document.body.appendChild(canvas);

let scene;
let scenes: any[] = [];

let eng = new Engine(canvas, true, {}, true);
let gui = menuScene(eng);
scenes[0] = createScene1(eng);
scenes[1] = createScene2(eng);
scenes[2] = createScene3(eng);
scenes[3] = createScene4(eng);
scene = scenes[0].scene;
setSceneIndex(0);

export default function setSceneIndex(i: number) {
  eng.runRenderLoop(() => {
      scenes[i].scene.render();
  });
}
```

## Scene Switching 
The setSceneIndex function allows switching between different scenes by changing the index of the scenes array. This function is called to render the selected scene in the render loop.

## GUI Scene
The gui folder contains the GUI scene, which provides a user interface to navigate between different scenes. The menuScene function initializes the GUI and sets up buttons to switch scenes.

```ts
import setSceneIndex from "./index";

import {
    Scene,
    ArcRotateCamera,
    Vector3,
    HemisphericLight,
    MeshBuilder,
    Mesh,
    Light,
    Camera,
    Engine,
    StandardMaterial,
    Texture,
    Color3,
    CubeTexture,
    Sound
  } from "@babylonjs/core";
  import * as GUI from "@babylonjs/gui";

function createSceneButton(scene: Scene, name: string, index: number, x: string, y: string, advtex) {
  // Implementation for creating a button to switch scenes
}

export default function menuScene(engine: Engine) {
  let scene = new Scene(engine);
  let advancedTexture = GUI.AdvancedDynamicTexture.CreateFullscreenUI("myUI", true);
  var button1 = createSceneButton(scene, "but1", 1, "-150px", "120px", advancedTexture);
  var button2 = createSceneButton(scene, "but2", 2, "-50px", "120px", advancedTexture);
  var button3 = createSceneButton(scene, "but3", 3, "50px", "120px", advancedTexture);
  var button4 = createSceneButton(scene, "but4", 4, "150px", "120px", advancedTexture);
  var camera = createArcRotateCamera(scene);

  let that: SceneData = {
    scene,
    advancedTexture,
    button1,
    button2,
    button3,
    button4,
    camera
  };

  return that;
}
```

This setup allows for a modular and organized way to manage multiple scenes within a single Babylon.js application.

