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


1. Draw Function: 
If the mouse isn’t pressed, the part.action() allow them to update their position and draw themselves.
Then, If the frame rate is above 50, it adds a new particle to the particles array.

(In this step, I want to use the same way in my project which means each stroke of an item can be represented by a particle object, when the user press the mouse, they can influence the particle swarm, and changes can occur to generate new strokes around the mouse.)
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

2. Key Press Function:
Use if/else statement to Toggle the animation, when the spacebar is pressed, it stops the loop, else, it resumes the loop.

(In this step, I want to use spacebar to control the animation of the project, users can pause or keep the animation going.) 
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

3. Particle Class:
In constructor(), creator defines the position and alpha of the particle, makes every particle randomly.
In action(), creator caculates the particle's current position to generate the 'a', then, use the cos(), sin() to control the speed of particle. If particle moves outside the canvas boundaries, a new particle is generated in a new location and the alpha value is random as well. Use img get() to get the color from the loaded image, and set up the alpha value for the color of the particle, finally, draw the ellipse particle in updated position.

(In thhis step, I want to use the class method to change the every position of the stroke, color of the stroke, movement of the stroke in my project.) 

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
