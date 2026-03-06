# GunroarCannon

**The 3D engine (physics+rendering) wrapper of three.js for people who find repeating code and boilerplate offensive.**

GunroarCannon is a lightweight, opinionated wrapper for **Three.js** and **Cannon-es**. It’s designed for developers who want to put a box in a digital void without spending forty-five minutes configuring a gravity vector or manually syncing quaternions like it's 1996.

---

## Why this exists

Calling `scene.add()`, `world.addBody()`, and then writing a `requestAnimationFrame` loop to copy positions from one to the other is a repetitive stress injury waiting to happen. GunroarCannon handles the marriage between physics and visuals so you can focus on more important things, like why your character's head is clipping through the floor.

---

## Features

* **Integrated Physics:** Automatic synchronization between Three.js meshes and Cannon-es bodies. If it moves in the world, it moves on the screen. Usually.
* **Lazy Loading:** One-line methods for loading GLTF, OBJ, FBX, STL, and Collada. It even tries to handle the materials so you don't have to.
* **Simple FPS Controls:** A camera controller that doesn't require a degree in linear algebra to navigate.
* **CSS3D Integration:** Stick a fully functional web browser or a React form inside your 3D world, because regular UI is for people who like things to be "readable" and "convenient."
* **Tweening/Easing:** A built-in animation system for those who want smooth transitions but can't be bothered to install yet another npm package.

---

## Quick Start

Made to be easy peasy. 

```javascript
import { GunroarCannon } from './GunroarCannon.js';

// Initialize the engine with physics enabled
const engine = new GunroarCannon({ 
    withPhysics: true 
});

// Add a box. It's a box. It's green.
const box = engine.addBox({
    size: [1, 1, 1],
    position: [0, 5, 0],
    mass: 1, // It falls. Gravity is real here.
    color: 0x00ff00
});

// Add a floor so the box doesn't fall into the infinite abyss
engine.addBox({
    size: [10, 0.1, 10],
    position: [0, 0, 0],
    mass: 0, // Static. Physics-speak for "immovable object."
    color: 0x444444
});

// Controls, because staring at a static screen is boring
engine.addControls('firstPerson');

```

---

## Loading Models

Manually setting up an `OBJLoader` is a great way to waste an afternoon. Use this instead:

```javascript
await engine.loadMesh('./assets/my_model.glb', {
    position: [0, 2, 0],
    physics: true,
    physicsOptions: { mass: 5 }
});

```

Supported Formats: `.gltf`, `.glb`, `.obj`, `.fbx`, `.stl`, `.dae`, `.ply`.

---

## The "Everything is a Panel" Feature

GunroarCannon allows you to inject HTML directly into the 3D scene. This is perfect for when you want to force users to fill out a survey while being attacked by physics-based spheres.

```javascript
import { createEnhancedBrowserPanel } from './GunroarCannon.js';

// Adds a literal web browser to your scene. 
// Performance? Maybe. Cool factor? Definitely.
const browser = createEnhancedBrowserPanel('https://github.com');

```

---

## Methods for the Perfectionist

| Method | What it does |
| --- | --- |
| `addBox(options)` | Creates a cube. Revolutionary. |
| `addSphere(options)` | Creates a sphere. Also revolutionary. |
| `animateCameraToMeshObject(mesh, duration)` | Smoothly moves the camera so you don't give your users motion sickness. |
| `physicsPaused` | A boolean for when you need the universe to stop while you think. |

---

## Known Issues

* The physics engine follows the laws of gravity. If your objects fly away, you probably set a negative mass or you've discovered a bug in `cannon-es` that I am definitely not going to fix.
* The "SimpleFPSControls" are indeed simple. Don't try to build the next *Call of Duty* with them.

## License

MIT. Use it for whatever you want. If you build something that makes a billion dollars, a "thank you" would be nice, but I'll settle for you not filing a GitHub issue when you forget to add a light to your scene and the screen is black.

**Next Step:** Would you like me to generate a `package.json` and a basic `index.html` to get this project running in a local environment?
