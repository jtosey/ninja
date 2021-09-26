

# CN Notes
## Playground
You can experiment with short JavaScript snippets no the [JavaScript Playground](https://playcode.io/).

## Variables have one of the following types:
### number
Numbers are rational numbers (negative, positive, zero, including integers).  Important operations:
```ts
let x = 1 + 2;            // "addition"; x is 3
let x = 3 - 1;            // "subtractions"; x is 2
let y = -x;               // "negation"; is is -2 (given above)
let x = 3 * 4;            // "multiplication"; x is 12
let x = 3 / 2;            // "division"; x is 1.5
let x = 2 ** 4;           // "exponentiation"; x = 2 * 2 * 2 * 2 = 16
let x = 5 % 3;            // "modulus" or "remainder"; x = 2; (5 / 3 = 1 remainder 2)
x++;                      // "increment"; given x was 2, it is now 3
x--;                      // "decrement"; given x was 3, it is now 2
```
Many of these can be combined as an abbreviation:
```ts
x += 1;                   // add one to x
x -= 1;                   // subtract one to x
x *= 2;                   // multiple x by 2
x /= 2;                   // divide x by 2
x %= 2;                   // modulus (or reminder), after dividing by x
```
You can compare these with:
```ts
x == y                    // equal
x != y                    // not equal
x < y                     // less
x <= y                    // less or equal
x > y                     // greater
x >= y                    // greater or equal
```
### strings
Strings are sequences of characters for creating words and sentences.  Important operations:
```ts
let x = "Hi" + " " + "Ed"; // "concatenation"; x is "Hi Ed"
x += "!";                  // append; x is now "Hi Ed!"
```
Strings can be compared similarly to numbers, with `==`, `!=`, `<=`, etc.
Confusingly, there are two different equality operators, `==` and `===`.
```ts
let x = 5 == "5";          // true, because they print the same
let x = 5 === "5";         // false, because they really are different (number vs a string)
```
### boolean
Booleans are either true or false (not capitalized). Important operations
```ts
let x = ! true;           // "not"; x is false
let x = false == false;   // comparison for equality; x is true
let x = true != false;    // comparison for inequality; x is true
let x = true && false;    // "and"; x is false
let x = false || true;    // "or"; x is true
```
A very popular operation is a ? b : c. Examples:
```ts
let x = true  ? "Yes" : "No"; // x is "Yes"
let x = false ? "Yes" : "No"; // x is "False"
```
Conveniently, numbers and strings can be converted to boolean with the `not`.
```ts
let x = ! 1;              // x is "not 1", which is false
let x = !! 1;             // converts 0 to false, everything else to true
let x = !! 37;            // similarly, x = true
let x = !! null;          // false
let x = !! "hello";       // true
```
### Bitwise
I won't go into this yet -- I don't think you need it yet.
### Objects or hashes
A hash lets translates a key (which is easy to remember) to a value (which is hard to remember).  Code Ninja uses this to convert keys or directions to numbers.  It sets up these definitions for you:
```ts
let Keys = {
  ...
  leftArrow  : 37, // Keys.leftArrow == Keys['leftArrow'] == 37
  upArrow    : 38, // Keys.upArrow == Keys['upArrow'] == 38
  rightArrow : 39, // etc
  downArrow  : 40, // etc
  ...
};
```
Thus:
```ts
if (isKeyPressed(Keys.leftArrow)) ...
```
Is the same as:
```ts
if (isKeyPressed(37)) ...
```
Similarly:
```ts
let Directions = {
  south      :   0, // Directions.south == Directions['south'] == 0
  southWest  :  45, // Directions.southWest == Directions['southWest'] == 45
  west       :  90, // etc
  northWest  : 135, // etc
  north      : 180, // etc
  northEast  : 225, // etc
  east       : 270, // etc
  southEast  : 315  // etc
};
```
## Functions
Functions have names, and optionally return values.  For instance:
```ts
function add(a, b) {
  return a + b;
}
```
Evaluates `add(3, 4) == 7`.  For documentation purposes, we sometimes add in the types, so that it is easier to understand what this does. This is how we would write documentation for this function.  This way you can tell you pass in a number (and not boolean), and that it returns a value.
```ts
// "add" returns a + b
function add(a: number, b: number): number;
```
If a function doesn't return anything, we say it returns `void`, or nothing:
```ts
// "log" a message to the console
function log(message: string): void;
```
Functions that don't have names are called `anonymous functions` (or lambda functions, because the guy who invented them was a mathematician who just used the next available Greek letter).

To use an anonymous function, you can assign it it a variable:
```ts
var add = function(a, b) { return a + b };
```
This is so incredibly popular that a more concise way of writing is now common. This means EXACTLY the same thing, but has less keystrokes. When you get comfortable with this, you'll use it a lot.
```ts
var add = (a, b) => a + b;
```
## Concept of a class
Objects with built-in functions are called classes.  You are using them a lot, but don't know it yet.  We'll learn more about this in an upcoming belt. In short:
* A class is a template, used to create similar objects, called instances. Eg., a Square class can be used to make a bunch of squares, each of a different size.
* Objects made from classes have properties, such as side-length.
* Objects made from classes have methods, which perform calculations.  Methods use this (or `$this`) to access the insides of the object.

Example:
```ts
class ScoreBoard {
   constructor() { this.curentScore = 0; }
   win()         { this.curentScore++; }
   lose()        { this.currentScore--; }
   score()       { return this.currentScore; }
}
```
You would use this as follows:
```ts
var scoreBoard = new ScoreBoard();
scoreBoard.win();
scoreBoard.win();
scoreBoard.lose();
let score = scoreBoard.score(); // returns 1
```
## How Game Objects Work
Code Ninja Games are made up of `GameObject`s which have:
* properties - e.g., width and height
* getters/setters - usually simple functions for modifying properties.  E.g., `var x = ball.x();` gets the ball's position, and `ball.x(300)` sets it to 300.
* methods - often more complicated functions which perform calculations.  All functions that are part of objects are often called methods, to separate them from functions which are not part of objects.
If you are working on an object you can "ask it to bounce" rather than "bouncing it". You
presently call it `$this`, but will eventually call it `this` (same as Python `self`):
```ts
if ($this.isTouchingWall()) {
  $this.bounce();
}
```
When manipulating another object, reference it by name, and ask it to "bounce":
```ts
if (circle.isTouchingWall()) {
  circle.bounce();
}
```
Let's look at several ways of modifying a property, all of which are used in this game.  First, let's suppose you're working with a `ScoreBoard` object that is tracking the score.  You can say this, to add one to the score:
```ts
$this.score += 1;
```
Sometimes you don't directly know the name of an object, but you know the name of another
object that does know about this object. For instance, a ball may now know what the score
is, but it would know about the scene it participates in, and that scene knows the score,
so a method in a ball can do this:
```ts
$this.scene.score.value += 1;
$this.scene.score.text(scene.score.value);
```
If it did know of the score directly, it could have just done this::
```ts
$this.score.value += 1;
$this.score.text(score.value);
```
Last, often used at the white belt level, is to assume that all objects are `global`, which means you can access them by name alone. You won't be able to do this much longer, as this is not a good practice.
```ts
score.value += 1;
score.text(score.value);
```
Normally methods are part of objects, but for reasons that are unclear to me, Code Ninja
also has "global" functions that you pass an object to. That is, you can say:
```ts
moveX(star, 10);
moveY(star, 20);
```
But it is much better to tell the star to move itself:
```ts
star.moveTo(10, 20);        // to location
star.moveToObject(target);  // to another object
```
### Base GameObject
Games are made up of Game Objects, which are instances of classes. All Game Objects have these features, but all sorts of specific types of Game Objects, including those that you make, will have more features.
```ts
class GameObject {

  name(string newName): void;         // name of object

  findName(name: string): GameObject; // find another gameObject in a group given its name (e.g., bullet)

  clone(): GameObject;                // add a duplicate of this object to the scene
  remove() void;                      // remove this object from the scene

  width(newWidth: number): void;      // n pixels wide
  height(newHeight: number): void;    // n pixels high

  offsetX(newX: number): void;        // offset of an object from its left (x-center)
                                      // often, but not always, its radius or half its width
  offsetY(newY: number): void;        // offset of an object from its top (y-center)
                                      // often, but not always, its radius or half its height

  offsetX(): number;                  // current X offset (x-center)
  offsetY(): number;                  // current Y offset (y-center)

  x(newX: number): void;              // move object to X
  y(newY: number): void;              // move object to Y
  z(newZ: number): void;              // move object to Z

  x(): number;                        // current X position
  y(): number;                        // current Y position
  z(): number;                        // current Z position

  scaleX(newX: number): void;         // multiply width by n; 1.0 is normal; use negative to flip
  scaleY(newY: number): void;         // multiply height by n; 1.0 is normal; use negative to flip

  scaleX(): number;                    // current X scaling factor
  scaleY(): number;                    // current Y scaling factor

  speedX(newSpeedX: number): void;     // set speed (pixels / frameUpdate) in X direction
  speedY(newSpeedY: number): void;     // set speed (pixels / frameUpdate) in Y direction

  speedX(): number;                    // current speed (pixels / frameUpdate) in X direction
  speedY(): number;                    // current speed (pixels / frameUpdate) in Y direction

  opacity(opactity: number): void;     // transparent = 1 ... opaque = 1

  rotation(degrees: number): void;     // rotate object by any angle, in degrees (0..359.99), where south = 0 (down)
  pointToObject(go: GameObject): void; // calculates the rotation necessary to point to another object
  pointToCursor(): void;               // calculates the rotation necessary to point to mouse cursor
  pointTo(x: number, y: number): void; // calculates the rotation necessary to point to (x, y)

  direction(direction: number): void;  // set heading as an angle; reference Directions.key (e.g., Directions.south)
  flipDirection(): void;               // flip heading by 180 degrees

  moveForward(speed: number): void;    // move in $this.direction() by speed pixels
  moveForwardByRotation(): void;       // move in direction of rotation by ($this.speedX(), $this.speedY());
  moveTo(x: number, y: number): void;  // move to (x, y)
  moveToObject(go: GameObject): void;  // move to (gameObject.x(), gameObject.y());

  findDistance(go: GameObject): number;// return distance to another object

  isTouching(go: GameObject): bool;    // returns "true" if object is touching an object; e.g., if (star.isTouchingl(ninja)) { ... }
  isTouchingWall(): bool;              // returns "true" if object is touching the wall; e.g., if (ball.isTouchingWall()) { ... }

  bounce(): void;                      // bounce off wall; e.g., ball.bounce();

  animation(sprit: stringe): void;     // name of an array of sprites, for animation
  incrementAnimation(): void;          // use the next sprite in the sprite array

  frameIndex(): number;                // return the current frame index
  frameIndex(index: number): void;     // show this sprint in the animation array

  fill(rgbColor: string): void;        // set the color to "#rrggbb" color string, where each color may be 00 (off) .. ff (on)
                                       // "#ff00ff" is bright red and blue, with no green, which is purple

  visible(): bool;                     // is current visible?
  visible(isVisible: bool): void;      // set visibility; e.g., visible(true) makes it visible
  toggleVisible(): void;               // same as $this.visible(! $this.visible());

  draggable(): bool;                   // is current draggable?
  draggable(isDraggable: bool): void;  // set draggable; e.g., draggable(true) makes it visible
  toggleDraggable(): void;             // same as $this.draggable(! $this.draggable());

  // many others ...
}
```
### Label
This is another type of `GameObject`, which has more features than the basic type. We normally write it this way, to indicate that Label is a `GameObject`, with extensions or additional superpowers:
```ts
class Label extends GameObject {
  void text(string aLabel);         // set the label to show aLabel.  e.g., label.text("Score:");
}
```
## Global functions
```ts
getMouseX(): number;                                 // current X position of the mouse
getMouseY(): number;                                 // current Y position of the mouse
isKeyPressed(key: number): bool;                     // e.g., Keys.rightArrow; returns true if currently pressed

spin(gameObject: GameObject, rate: number): void;    // each frameUpdate rotate "gameObject" by "rate"?

moveX(gameObject: GameObject): void;                 // move "gameObject" by "gameObject.speedX"
moveY(gameObject: GameObject): void;                 // move "gameObject" by "gameObject.speedY"

moveX(gameObject: GameObject, pixels: number): void; // move "gameObject" to the right (if positive)
moveY(gameObject: GameObject, pixels: number): void; // move "gameObject" down (if positive)

bounce(gameObject: GameObject): void;                // change direction by 180 degrees

random(choices: number): number;                     // return a number from 0 .. (choices - 1)
random(max: number, min: number):number              // return a number from min .. max, inclusive

parseInt(value: string): number;                     // returns the number in the string; parseInt("10") === 10
Math.round(n: number) :number;                       // returns rounded off number; e.g., round(5.6) === 6.0

createTimer(period_ms: number, expiry: func): void;  // call "expiry" every "period_ms" which is in milliseconds
```
### Comments
With objects, we say that some objects are _containers_ and hold other objects". E.g., the "scene" has all sorts of objects that are part of the game in it. When a frameUpdate occurs, the game engine ask the scene to paint itself. The scene then asks all the objects that it contains to paint themselves (e.g., robot, floor). The robot may also be a container with arms and legs, and will ask each of them to paint themselves ... etc.


