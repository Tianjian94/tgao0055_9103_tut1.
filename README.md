# tgao0055_9103_tut1.

## Imaging Technique Inspiration 
### Screenshots

![Image of starry night 1](asset/Van%20Gogh1.png)
![Image of starry night 2](asset/Van%20Gogh2.png)

### This is the link of video 
[Petros vrellis Starry night interactive animation (2012)](http://artof01.com/vrellis/works/starry_night.html) 

- This is a large interactive installation that The viewer is further engaged by interacting with the painting; almost infinite variations can occur, as the flows are driven by his hand. 

- In this artwork, I want to combine two aspects in my project, one is infinite variation or rotation of the line, another is user interaction. 

- Generallly speaking, when the user uses the mouse or touches the screen, the elements on the screen change in real time

- Benefits: The flow of elements in the screen can make the project more vivid and interesting, and the interaction between the user and the project can increase the interactivity and make the user more immersive

## Coding Technique Exploration

[Code example (starry night)](https://openprocessing.org/sketch/1209499)

! [Image of the starry night](asset/starry%20night.png)

! [Image of the starry night2](asset/starry%20night2.png)

1. Global Variables: 
Creator set up the global variables, includes 'particles', 'noiseScale', 'speed', 'o'.
``` 
let particles = [];
let noiseScale = 400;
let speed = 0.1;
let o = 0;
```

2. Preload Function: 
Set up image 'starry night.jpg' 
```
function preload() {
    img = loadImage('starry night.jpg');
}
```

3. Setup Function: 
Set up the canvas size, background, nostroke, for loop (add 100 particle to the particles array)
```
function setup() {
    createCanvas(757, 600);
    background(0);
    noStroke();
    for (i = 0; i < 100; i++) {
        particles.push(new p());
    }
}
```

4. Draw Function: 
If the mouse isn’t pressed, the part.action() allow them to update their position and draw themselves.
Then, If the frame rate is above 50, it adds a new particle to the particles array, 

```
function draw() {
    if (!mouseIsPressed) {
        mouseX = noise(frameCount / 100) * width;
        mouseY = noise(frameCount / 100 + 100) * height;
    }
    for (i = 0; i < 10; i++) {
        for (let part of particles) {
            part.action();
        }
    }
    if (frameRate() > 50) {
        particles.push(new p());
    }
    for (i = 0; i < 10; i++) {
        if (particles[int(random(100))].lt > 200) {
            particles[int(random(100))].pos = createVector(mouseX + random(-50, 50), mouseY + random(-50, 50));
            particles[int(random(100))].lt = 0;
        }
    }
}
```

5. Key Press Function:
Use if/else statement to Toggle the animation 
```
function keyPressed() {
    if (keyCode == 32) {
        if (o == 1) {
            noLoop();
            o = 0;
        } else {
            loop();
            o = 1;
        }
    }
}
```

