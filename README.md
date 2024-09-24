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

![Image of the starry night](asset/starry%20night.png)

![Image of the starry night2](asset/starry%20night2.png)

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
Set up the canvas size, background(), nostroke(), for loop (add 100 particle to the particles array)
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
Use if/else statement to Toggle the animation, when the spacebar is pressed, it stops the loop, else, it resumes the loop. 
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

6. Particle Class:
In constructor(), creator defines the position and alpha of the particle, makes every particle randomly.
In action(), creator caculates the particle's current position to generate the 'a', then, use the cos(), sin() to control the speed of particle. If particle moves outside the canvas boundaries, a new particle is generated in a new location and the alpha value is random as well. Use img get() to get the color from the loaded image, and set up the alpha value for the color of the particle, finally, draw the ellipse particle in updated position. 

```
class p {
    constructor() {
        this.pos = createVector(random(0, width), random(0, height));
        this.alpha = random(-50, 50);
        this.lt = 0;
    }
    action() {
        let a = noise(this.pos.x / noiseScale, this.pos.y / noiseScale) * 2 * PI * noiseScale;
        this.pos.x += cos(a) * speed;
        this.pos.y += sin(a) * speed;
        if (this.pos.x < 0 || this.pos.x > width || this.pos.y < 0 || this.pos.y > height) {
            this.pos = createVector(random(0, width), random(0, height));
            this.alpha = random(-50, 50);
        }
        let c = img.get(int(this.pos.x), int(this.pos.y));
        fill(red(c) + this.alpha, green(c) + this.alpha, blue(c) + this.alpha);
        ellipse(this.pos.x, this.pos.y, 5);
        this.lt++;
    }
}
```
