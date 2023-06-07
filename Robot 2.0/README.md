# Robot 2.0 :robot: :rocket:

Welcome to the Robot 2.0 tutorial! :wave:

This tutorial is based on the Robot 2.0 repository and aims to guide you through character motion and animation in a 2D game. Get ready for an exciting journey! :video_game:

## Overview

In this tutorial, you'll learn how to create a 2D game character that exhibits smooth motion and animation. The provided code snippet demonstrates the implementation of a robotic character with dynamic eye movements and body animation.

Let's break down the code and dive into the details:

## Canvas Setup

The first part of the code initializes the canvas and its rendering context. It sets up the canvas with a width of 600 pixels and a height of 800 pixels. The stroke style is set to "white" with a line width of 3 pixels. This ensures that the subsequent drawings on the canvas have the desired appearance.

```javascript
// Canvas setup
const canvas = document.getElementById("canvas1");
const ctx = canvas.getContext("2d");
canvas.width = 600;
canvas.height = 800;
ctx.strokeStyle = "white";
ctx.lineWidth = 3;
```

## the constructor of the "Robot" 🤖 class

🤖 The `Robot` constructor initializes the properties of a robot instance:

- 💡 `this.canvas = canvas;`: Assigns the canvas parameter to the canvas property of the Robot instance.

- 🌐 `this.x = this.canvas.width * 0.4;`: Sets the initial x-coordinate of the robot's position on the canvas to 40% of the canvas width.

- 🌍 `this.y = this.canvas.height * 0.5;`: Sets the initial y-coordinate of the robot's position on the canvas to 50% of the canvas height.

- 🔍 `this.centerX = this.x;`: Assigns the current x-coordinate as the center x-coordinate of the robot.

- 🔍 `this.centerY = this.y;`: Assigns the current y-coordinate as the center y-coordinate of the robot.

- 📏 `this.radius = 80;`: Sets the radius of the robot (used for eye positioning and other calculations).

- 🌀 `this.angle = 0;`: Sets the initial angle of the robot (used for eye positioning and animations).

- 🖼️ `this.spriteWidth = 370;`: Sets the width of the robot's body sprite.

- 🖼️ `this.spriteHeight = 393;`: Sets the height of the robot's body sprite.

- 🎞️ `this.frameX = 0;`: Sets the current frame of the robot's animation (used for sprite sheet animation).

- 🎞️ `this.maxFrame = 75;`: Sets the maximum number of frames in the robot's animation (used for sprite sheet animation).

- 🖼️ `this.bodyImage = document.getElementById("body");`: Retrieves the HTML element with the ID "body" and assigns it to the bodyImage property.

- 🖼️ `this.bodySprite = document.getElementById("bodySprite");`: Retrieves the HTML element with the ID "bodySprite" and assigns it to the bodySprite property.

- 👁️ `this.eye1Image = document.getElementById("eye1");`: Retrieves the HTML element with the ID "eye1" and assigns it to the eye1Image property.

- 👁️ `this.eye2Image = document.getElementById("eye2");`: Retrieves the HTML element with the ID "eye2" and assigns it to the eye2Image property.

- 💡 `this.reflectionImage = document.getElementById("reflection");`: Retrieves the HTML element with the ID "reflection" and assigns it to the reflectionImage property.

- 💡 `this.detectorLightImage = document.getElementById("detectorLight");`: Retrieves the HTML element with the ID "detectorLight" and assigns it to the detectorLightImage property.

- 👁️ `this.eye1Radius = this.radius * 0.4;`: Calculates the radius of eye1 based on the robot's radius.

- 👁️ `this.eye2Radius = this.radius * 0.65;`: Calculates the radius of eye2 based on the robot's radius.

- 👁️ `this.eye1Distance = this.eye1Radius;`: Sets the initial distance of eye1 from the robot's center.

- 👁️ `this.eye2Distance = this.eye2Radius;`: Sets the initial distance of eye2 from the robot's center.

- 🔎 `this.tracking = false;`: Sets the initial tracking state of the robot (used for determining if the robot is tracking the mouse).

- 🔄 `this.movementAngle = 0;`: Sets the initial movement angle of the robot (used for animations).

- 🖱️ `this.mouse = { x: 0, y: 0 };`: Sets the initial mouse coordinates to (0, 0)

 (used for tracking mouse movement).

This constructor initializes the properties of a `Robot` instance, including its position, size, sprite images, and various other variables used for animation and tracking. 😊

```javascript
constructor(canvas) {
  this.canvas = canvas;
  this.x = this.canvas.width * 0.4;
  this.y = this.canvas.height * 0.5;
  this.centerX = this.x;
  this.centerY = this.y;
  this.radius = 80;
  this.angle = 0;
  this.spriteWidth = 370;
  this.spriteHeight = 393;
  this.frameX = 0;
  this.maxFrame = 75;
  this.bodyImage = document.getElementById("body");
  this.bodySprite = document.getElementById("bodySprite");
  this.eye1Image = document.getElementById("eye1");
  this.eye2Image = document.getElementById("eye2");
  this.reflectionImage = document.getElementById("reflection");
  this.detectorLightImage = document.getElementById("detectorLight");
  this.eye1Radius = this.radius * 0.4;
  this.eye2Radius = this.radius * 0.65;
  this.eye1Distance = this.eye1Radius;
  this.eye2Distance = this.eye2Radius;
  this.tracking = false;
  this.movementAngle = 0;
  this.mouse = {
    x: 0,
    y: 0,
  };
}
```
## 🔄 Updating Robot 🤖 Properties and Animation 🔧 

- 🔄 `const dx = this.mouse.x - this.x;`: Calculates the horizontal distance between the robot's current x-coordinate and the mouse's x-coordinate.

- 🔄 `const dy = this.mouse.y - this.y;`: Calculates the vertical distance between the robot's current y-coordinate and the mouse's y-coordinate.

- 📏 `const distance = Math.hypot(dx, dy);`: Calculates the Euclidean distance between the robot and the mouse using the Pythagorean theorem.

- 🔍 `this.angle = Math.atan2(dy, dx);`: Calculates the angle between the robot and the mouse using the `Math.atan2()` function.

- 🔄 `if (distance <= this.eye1Distance * 2.5) { ... }`: Checks if the distance between the robot and the mouse is within a certain range.

  - 👁️ `this.eye1Radius = distance * 0.4;`: Adjusts the radius of eye1 based on the distance between the robot and the mouse.
  
  - 👁️ `this.eye2Radius = distance * 0.65;`: Adjusts the radius of eye2 based on the distance between the robot and the mouse.
  
- 🔄 `else if (this.tracking) { ... }`: If the robot is currently tracking the mouse:

  - 👁️ `this.eye1Radius = this.eye1Distance;`: Resets the radius of eye1 to its original distance from the robot's center.
  
  - 👁️ `this.eye2Radius = this.eye2Distance;`: Resets the radius of eye2 to its original distance from the robot's center.
  
- 🔄 `else { ... }`: If the robot is not tracking the mouse:

  - 👁️ `this.eye1Radius = this.eye1Distance * Math.cos(this.movementAngle);`: Adjusts the radius of eye1 based on the movement angle of the robot.
  
  - 👁️ `this.eye2Radius = this.eye2Distance * Math.cos(this.movementAngle);`: Adjusts the radius of eye2 based on the movement angle of the robot.
  
- 🎞️ `this.frameX >= this.maxFrame ? (this.frameX = 0) : this.frameX++;`: Updates the frame of the robot's animation, resetting it to 0 if it exceeds the maximum frame.

- 🔄 `this.movementAngle += 0.005;`: Increments the movement angle of the robot.

- 🔍 `this.x = this.centerX + Math.cos(this.movementAngle * 3) * 80;`: Updates the robot's x-coordinate based on its center x-coordinate and a circular motion.

- 🔍 `this.y = this.centerY + Math.sin(this.movementAngle * 0.5) * 150;`: Updates the robot's y-coordinate based on its center y-coordinate and a circular motion.

- 📣 `console.log(this.movementAngle);`: Outputs the current movement angle to the console.

- 🔄 `if (this.movementAngle > Math.PI * 4) { ... }`: Checks if the movement angle exceeds a full circle.

  - 📣 `console.log("RESET");`: Outputs "RESET" to the console.
  
  - 🔄 `this.movementAngle = 0;`: Resets the movement angle to 0.
  

The `update()` method performs calculations and updates the properties of the `Robot` instance based on the position of the mouse, animation frames, movement angles, and circular motion.

```javascript
    update() {
      const dx = this.mouse.x - this.x;
      const dy = this.mouse.y - this.y;
      const distance = Math.hypot(dx, dy);
      this.angle = Math.atan2(dy, dx);
      if (distance <= this.eye1Distance * 2.5) {
        this.eye1Radius = distance * 0.4;
        this.eye2Radius = distance * 0.65;
      } else if (this.tracking) {
        this.eye1Radius = this.eye1Distance;
        this.eye2Radius = this.eye2Distance;
      } else {
        this.eye1Radius = this.eye1Distance * Math.cos(this.movementAngle);
        this.eye2Radius = this.eye2Distance * Math.cos(this.movementAngle);
      }
      this.frameX >= this.maxFrame ? (this.frameX = 0) : this.frameX++;
      this.movementAngle += 0.005;
      this.x = this.centerX + Math.cos(this.movementAngle * 3) * 80;
      this.y = this.centerY + Math.sin(this.movementAngle * 0.5) * 150;
      console.log(this.movementAngle);
      if (this.movementAngle > Math.PI * 4) {
        console.log("RESET");
        this.movementAngle = 0;
      }
    }
  }
  ```
## 🎬 Animation Loop Execution 🔄🎨

Explanation: The provided code snippet sets up an animation loop using the `requestAnimationFrame()` method to continuously update and render the robot on the canvas. Here's a breakdown of the steps involved:

1. 🤖🎨 `const robot = new Robot(canvas);`: Creates a new `Robot` instance by calling the `Robot` constructor, passing the `canvas` element as an argument. This initializes the robot with its initial properties.

2. 🎬🔄 `function animate() { ... }`: Defines the `animate()` function, which serves as the animation loop. This function will be called recursively to update and redraw the robot.

3. 🖌️🧹 `ctx.clearRect(0, 0, canvas.width, canvas.height);`: Clears the entire canvas by using the `clearRect()` method of the rendering context (`ctx`). This ensures that the previous frame's content is removed, providing a clean canvas for the new frame.

4. 🖌️🤖 `robot.draw(ctx);`: Invokes the `draw()` method of the `robot` instance, passing the rendering context (`ctx`) as an argument. This draws the robot on the canvas based on its current properties and state.

5. 🔄🤖 `robot.update();`: Invokes the `update()` method of the `robot` instance. This updates the robot's properties, such as position, animation frames, and eye radii, based on various calculations and conditions.

6. 🎥🔄 `requestAnimationFrame(animate);`: Requests the browser to call the `animate()` function recursively, allowing for smooth animation. This creates a loop where each frame triggers the subsequent frame.

7. ▶️🎬 `animate();`: Initiates the animation loop by calling the `animate()` function for the first time. This starts the continuous rendering and updating of the robot.

Overall, this code snippet sets up and executes an animation loop that repeatedly clears the canvas, draws the robot, updates its properties, and requests the next frame to be rendered. This creates the illusion of continuous animation.
  
  
  ```javascript
  const robot = new Robot(canvas);
  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    robot.draw(ctx);
    robot.update();
    requestAnimationFrame(animate);
  }
  animate();
});
```
## All Of Us Come From Soil, Feed Upon Soil and Go Back To Soil, So Please Save Soil🌱
