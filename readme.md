# ESP-IO

ESP-IO is an IO Plugin that enables writing JavaScript Robotics programs with Johnny-Five, which interact with ESP8266 boards.

## Boilerplate Programs

These are just conceptual use case sketches for now...

#### Using a single ESP8266

```js
var five = require("johnny-five");
var ESP = require("esp-io");
var board = new five.Board({
  io: new ESP()
});

board.on("ready", function() {
  // This is running on a local machine that's connected to an ESP8266
});
```

#### Using multiple ESP8266

This is how you might coordinate two ESP8266 boards with an Arduino (it doesn't matter what board you coordinate with, this was just for illustration):

```js
var boards = new five.Boards([
  { id: "arduino-or-whatever" }, 
  { id: "a", io: new Esp({ id: "a" }) }, 
  { id: "b", io: new Esp({ id: "b" }) }, 
]);

boards.on("ready", function() {
  var [arduino, a, b] = this; // *

  var threshold = 40; // degrees celsius
  var slider = new five.Sensor({
    pin: "A0", 
    board: arduino, 
    scale: [20, 40]
  });

  var thermometer = new five.Thermometer({
    controller: "TMP102",
    board: a
  });  

  var alarm = new five.Relay({
    pin: 5, // "D5" ?
    board: b
  });  

  thermometer.on("change", function() {
    if (this.c >= slider.value) {
      alarm.on();
    } else {
      alarm.off();
    }
  });
});
```


\* Same as: 

```js
var arduino = this[0];
var a = this[1];
var b = this[2];
```
