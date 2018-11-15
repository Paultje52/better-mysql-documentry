---
description: 'Every code section, please wait a moment'
---

# Queue

Better-MySQL is using a custom queue. You can use this too, if you want!

## Constructor

First, let's start off with the constructor. You can give up the interval, but if you don't do that, the interval is `500ms`. Here is a example.

```javascript
const betterMysql = require("better-mysql");
let queue = new betterMysql.queue(250); // Sets the interval to 250 MS.
```

## Add

The most important function: The add function. With the add function, you have to give up a function. That function will be called when its time for that. Here is a example.

```javascript
const betterMysql = require("better-mysql");
let queue = new betterMysql.queue(250); // Sets the interval to 250 MS.

queue.add(() => {
    console.log(1);
});
queue.add(() => {
    console.log(2);
});
queue.add(() => {
    console.log(3);
});
```

## Clear

The name does what it says: it's clearing the queue.

```javascript
const betterMysql = require("better-mysql");
let queue = new betterMysql.queue(250); // Sets the interval to 250 MS.

queue.add(() => {
    console.log(1);
});
queue.add(() => {
    console.log(2);
});
queue.add(() => {
    console.log(3);
});

queue.clear();
```

## Stop

If you want to stop or pause the interval, you can do that with the stop function. 

```javascript
const betterMysql = require("better-mysql");
let queue = new betterMysql.queue(250); // Sets the interval to 250 MS.

queue.add(() => {
    console.log(1);
});
queue.add(() => {
    console.log(2);
});
queue.add(() => {
    console.log(3);
});

queue.stop();
```

## Start

You stopped the queue, and now you want to start it. That is possible with the `queue.start` function. Here is a example.

```javascript
const betterMysql = require("better-mysql");
let queue = new betterMysql.queue(250); // Sets the interval to 250 MS.

queue.add(() => {
    console.log(1);
});
queue.add(() => {
    console.log(2);
});
queue.add(() => {
    console.log(3);
});

queue.stop();
setTimeout(() => {queue.start()}, 5000);
```

