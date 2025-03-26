---
layout: post
title: "Argy - The Diver Spider"
date: 2025-01-26
categories: [Gamejam,GroupProject]
tags: [C#,Unity]
image:
  path: /assets/Argy.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Splash art.
---

## About
"Argy: The Diver Spider" is a 2D platform game inspired by the homonymous spider that has the ability to create air bubbles whenever needed.

## Project info
**👤 Role:**  Lead programmer  
**👥 Team size:**  6  
**⏱︎Time frame:**  3 days
**⚒︎ Engine:**  Unity(C#)  

In this game, Argy, a diver spider, left his home in search of food supplies but was injured. Swim, avoid obstacles, manage oxygen by staying inside your bubble, and make your way back home.

### Swim
This method handles the swimming mechanics for the player. It applies a force to the character's Rigidbody based on the player's input (both horizontal and vertical movement). The vertical swimming force is adjusted depending on whether the character is swimming up or down.
```
void Swim()
{
    //Debug.Log(rb.velocity);

    // Imposta la velocità finale (mantieni la velocità verticale invariata)
    //rb.velocity = new Vector2(0f, 0f);
    ////rb.AddForce(new Vector2(, 0), ForceMode2D.Impulse);
    FindObjectOfType<AudioManager>().waitPlaying("Jump_Swim");
    if(movementInput.y > 0){
        rb.AddForce(new Vector2(movementInput.x * swimmingForce, movementInput.y * swimmingForce * 0.35f), ForceMode2D.Impulse);
    }else{
        rb.AddForce(new Vector2(movementInput.x * swimmingForce, movementInput.y * swimmingForce * 1.15f), ForceMode2D.Impulse);
    }

    lastImpulseTime = Time.time;
}
```

## What i learned
This was my first game jam, a unique experience where you have to think differently—there’s no time to create everything, so you must keep it simple while still aiming for something fun, original, and engaging. 

## More about...
Build, source code and further insights can be found in the github repository [here](https://github.com/GianluDR/ProjectJam).
