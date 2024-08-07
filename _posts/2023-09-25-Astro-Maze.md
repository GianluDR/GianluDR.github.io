---
layout: post
title: "Astro Maze: Coin-op puzzle game"
date: 2023-09-25
categories: [University,ThesisProject]
tags: [C#,Unity,Aseprite]
image:
  path: /assets/gameplay.gif
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Gameplay scene.
---

### About
Astro Maze is a **puzzle-arcade** game with platforming and roguelike elements that challenges the player to solve as many **procedurally generated mazes** as possible in the shortest amount of time. Will they manage to escape before the black hole engulfs the maze?  

## Project info
**👤 Role:**  Game programmer  
**👥 Team size:**  1  
**⏱︎Time frame:**  3 months  
**⚒︎ Engine:**  Unity(C#)

This game presented a significant challenge that made me put a lot of effort into **optimization** and in-depth understanding of **procedural generation algorithms**.

Developing this game independently was fun and educational. However, I find that working in a **group is better**. It allows you to share ideas, manage the workload better, and learn by collaborating with others.
<img src="/assets/eventFog.gif" width="50%" height="50%" alt="Gameplay footage showing event fog effect in Astro Maze.">

### Procedural Generation
To create an always solvable puzzle with minimal time complexity, I approached the maze as a tree structure. The starting position of the player served as the root, and reachable positions from that point were considered the leaves. I implemented a specialized **Breadth-First Search (BFS)** algorithm incorporating an **explored set**.

<img src="/assets/maze2.png" width="30%" height="30%" alt="A procedurally generated maze example from Astro Maze.">
The algorithm begins by searching the first reachable positions and adds them to a queue, ensuring to check against the explored set to avoid redundancy. It continues this process until the queue is empty or the goal is achieved.

```
private int mapSolution(){
        int i = 0;
        int n = -1;
        pathExist = false;
        Queue myQ = new Queue();
        myQ.Enqueue(start);
        visitedTiles.Add(start);
        while(myQ.Count > 0 && i < 500){
            myQ = exploreTilemap(myQ);
            if(myQ.Contains(exit) && !pathExist){
                n = i;
                pathExist = true;
            }
            i++;
        }
        return n;
    }
```

<img src="/assets/maze3.png" width="30%" height="30%" alt="Another maze layout from Astro Maze showing wall placements.">
In parallel, the algorithm's second part involves strategically placing walls in positions that are not reachable by the player. This technique enhances the overall map layout, ensuring a more engaging gameplay experience.


### Movement physics
Implementing smooth and intuitive movement mechanics was another crucial aspect of the project. I introduced limitations on movement dynamics to ensure the experience i envisioned. When the player initiates movement, they cannot immediately change direction; however, they can queue the next move. Once the player-directed cube reaches a wall, the next queued move is executed, or if the player inputs a new move, the cube responds by moving in that specified direction. 

```
var map = inputControl.currentActionMap;
bool touchPressed = map.FindAction("TouchPress", true).IsPressed();
if(!touchPressed){
    startPos = Vector2.zero;
    startPosInQ = Vector2.zero;
}
if (touchPressed){
    if(!isMoving){
        if(startPos == Vector2.zero)
            startPos = movementInput;
        var distance = Vector2.Distance(startPos, movementInput); 
        if (distance > 30){
            Vector2 direc = movementInput - startPos;
            direc = direc.normalized;
            direction = SwipeDetection(direc);
        }
    }

    if(startPosInQ == Vector2.zero)
        startPosInQ = movInQ;
    var distanceInQ = Vector2.Distance(startPosInQ, movInQ);
    if(distanceInQ > 30){
        Vector2 lastDirec = movInQ - startPosInQ;
        lastDirec = lastDirec.normalized;
        lastDir = SwipeDetection(lastDirec);
    }
}
```

## What i learned
This thesis work was an individual work that allowed me to explore the use of **procedural generation algorithms**. Astro Maze was an ideal platform to apply the knowledge and skills acquired during my academic journey. The experience enriched me tremendously, providing me with a comprehensive understanding of procedural algorithms and their role in creating dynamic gameplay. In addition, I conducted a playtesting session of the game using the **GEQ (Game Experience Questionnaire)**, this process allowed me to gain a deeper understanding of how players interacted with the game, their overall experience, and the specific aspects of gameplay they most liked or disliked.

Build, source code and further insights can be found in the github repository [here](https://github.com/GianluDR/AstroMaze).
