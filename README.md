## Phy.js - Minimal physics engine with an event loop

I created Phy.js because I couldn't install an archaic Python library on my Linux machine. All I wanted to do was to put a ball (circle) on the screen and make it react to forces.

Here's what you can do with Phy.js

### Examples

Make the ball go around in a circle:

```javascript
var canvas = getElementById('canvas');
var ctx = canvas.getContext('2d');

var ball = new Circle(ctx, new V(100, 100));  // <x,y> = <100,10>
var v = new Vector(2, 0);  // Force: 2 units to the right.

var main = function(dt, frame, time) {
    clearCanvas(c, ctx);
    ball.move(v).draw();
    v = v.rot(2);  // Rotate the vector 2 degrees.
}

eventLoop(main);
```

Gravity:

```javascript
// Init
var c = document.getElementById('c');
var ctx = c.getContext('2d');

// Objects
var planet = new Circle(ctx, new V(100, 100));
var sun = new Circle(ctx, new V(500, 500));

// Masses and distances
var Mp = 10;
var Ms = 100;
var d = planet.pos().dist(sun.pos());

// Forces
var Vp = new V(-10, 10);

// Main function
var main = function(dt, frame, time) {
    clearCanvas(c, ctx);
    
    planet.draw();
    sun.draw();

    var direction = planet.pos().sub(sun.pos()).mul(-1);
    var gravity = direction.mul(Mp * Ms / Math.pow(d, 2));

    Vp = Vp.add(gravity);
    planet.move(Vp);
}

eventLoop(main);
```

You can check out the "Gravity" demo here: [Phy.js Gravity demo](http://whoeverest.github.io/phy.js/index.html)