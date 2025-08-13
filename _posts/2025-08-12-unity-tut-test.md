---
layout: post
title: Unity Tutorial Test
date: 2025-08-12 14:24:00
description: this is what included plotly.js code could look like
tags: code
categories: sample-posts
featured: true
disqus_comments: true
chart:
  plotly: true
images:
  compare: true
  slider: true
---
### Introduction

Unity provides developers with tools to read user inputs like keystrokes, mouse movement, controller buttons, or touch events for interactions in their games. For years, Unity relied on the legacy input system, often referred to as the Old Input System. As games evolved and began supporting more complex control schemes and multiple devices, Unity introduced the New Input System to overcome the limitations of the legacy approach.

The Old Input System uses the static UnityEngine.Input class to read user inputs. It operates through polling, meaning that you query the input state manually every frame using Update() or similar functions. This system has been available since Unity’s early versions and is familiar to most Unity users. It’s lightweight and requires no setup, making it ideal for simple prototypes or when working with just a keyboard and mouse.

### Old Input System
Here's an example of reading input from the keyboard using this system: 

```c#
using UnityEngine;
 
public class CheckButtonPress : MonoBehaviour
{
 
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space)) 
           Debug.Log("Space was pressed this frame");
 
    }
 
}
```
The above code simply reads every time the space bar is pressed. The KeyCode enum stores the type of key the function should be checking. There are variations of the GetKeyDown() function such as GeyKey() which will check if the button is being held down and GetKeyUp() which returns if the button has been released. Try out some of the different combinations of these functions and the KeyCodes!

While you could use the above to check if a certain key is pressed, and then to apply some movement to the player, there is a better method in the older input system. Let's write out a basic example to control a cube's movement in Unity. First, go to your Unity hierarchy and add a cube. Next, create a new script called OldInputMovement. Then, write out the following to your script: 

```c#
using UnityEngine;
 
public class OldInputMovement : MonoBehaviour
{
    public float speed = 5.0f;
 
    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        Vector3 movement = new Vector3(h, 0, v);
        transform.Translate(movement * speed);
    }
}
```
 The above code uses Input Axes which are predefined in Unity. These are located and can be modified in Edit > Project Settings > Input Manager. These include horizontal, vertical, fire1, etc, and are tied to default values that correspond to their respective axes. For instance, horizontal typically corresponds to A & D for keyboard, or left and right on a controller and so on and so forth.

When you save and run the scene, the cube will start moving in the direction of the keys on your keyboard! Note: Make sure to press anywhere in the game window! If you don't Unity won't register the key presses from your keyboard. Similarly to when you tab out of a video game, what you do outside of the game window won't affect what happens in the game.

As you can see in the code, the values read from the GetAxis() function return a float value. This value ranges from -1 to 1 where the sign indicates the direction of movement. As I mentioned earlier, this code is pretty generic, as it isn't limited to ONLY your keyboard. In fact, grab a controller and connect it to your computer. You'll see that the controller's inputs on the joystick are also read as horizontal and vertical inputs!

At this point, you're probably wondering why your character is flying way too fast off-screen even if you change the speed. Remember about how fast Update's function is getting called. If your game is running at 60 fps, this function will be called 60 times per second. We aren't trying to calculate the cube's speed per frame!! Furthermore, on one computer, if your game can run faster, it would mean that your player also runs faster! We want the speed of the player to be consistent on all platforms! In other words, we need to make our code frame rate independent, meaning regardless of the frame rate of the game, the cube should ALWAYS move at the same speed. In order to make the proper conversion, you should utilize Time.deltaTime. Time.deltaTime returns how many seconds it takes to go from one frame to the next.

If my game runs at 60fps on my computer, but 180fps on yours, the Time.deltaTime is 0.0167 seconds and 0.00556 seconds respectively. Multiplying our speed by Time.deltaTime within update ensures that, regardless of the frame rate, the cube will ALWAYS move at the same pace.

```c#
using UnityEngine;
 
public class OldInputMovement : MonoBehaviour
{
    public float speed = 5.0f;
 
    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        Vector3 movement = new Vector3(h, 0, v);
        transform.Translate(movement * speed * Time.deltaTime);
    }
}
```
Despite the ease of use of this input system, its limitations quickly become apparent as you try to scale up: 
- It does not scale well with multiple input devices.
- Input rebinding requires a custom implementation.
- Device support (e.g., touch, VR, multiple controllers) is minimal.
- No native event-based input—everything is checked per frame.

### New Input System

As the gaming industry shifted toward supporting multiple input devices, cross-platform controls, and complex input schemes, Unity’s old system couldn't support dynamic rebinding, gamepad layouts, or input buffering easily. Unity's new input system solves these challenges with: 

- Action maps that separate controls from behavior.
- Support for all modern input devices (keyboard, mouse, touch, gamepad, XR, etc.).
- Event-driven architecture as well as polling.
- Serialized Input Assets for easy data-driven setup.

 The New Input System in Unity is built around a different approach from the legacy version. Rather than directly polling input from static classes like Input.GetKey(), the new system introduces a data-driven and event-based input that separates input definitions from gameplay logic. This design allows developers to define what inputs mean (like “Jump” or “Move”) in a centralized, reusable format called an Input Actions Asset. Inside this asset, inputs are organized into action maps, which can represent different control modes (such as “Player”, “UI”, or “Vehicle”)—each containing a collection of named Input Actions.

Each Input Action represents a high-level action the player can perform, such as moving a character or firing a weapon. Instead of hardcoding which key or button triggers the action, the action is bound to multiple control inputs. For instance, the “Jump” action could be triggered by the spacebar, the A button on an Xbox controller, or a screen tap on a mobile device. These bindings can be customized, added, or removed visually using the Input Actions editor in the Unity Inspector, and they support advanced features like composite bindings (e.g., WASD for 2D movement), control schemes (keyboard vs gamepad layouts), and binding groups for multiplayer setups.

Before we work on an example, let's make sure Unity has the new input system installed. Note: If you have Unity 6 or above, the following step is not necessary! Unity has moved completely to the new input system in Unity 6. 

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/9.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/7.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/8.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/10.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/12.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>

## Image Comparison Slider

This is a simple image comparison slider. It uses the [img-comparison-slider](https://img-comparison-slider.sneas.io/) library. Check the [examples page](https://img-comparison-slider.sneas.io/examples.html) for more information of what you can achieve with it.

<img-comparison-slider>
  {% include figure.liquid path="assets/img/prof_pic.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/prof_pic_color.png" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
