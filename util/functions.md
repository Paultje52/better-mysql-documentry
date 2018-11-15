---
description: Some functions for if you are using better-MySQL!
---

# Functions

> I suggest to only use those functions if you are also using the package main intention.

First, let's get the main function object. In this object there are different functions. You can get this object with this code.

```javascript
const betterMysql = require("better-mysql");
let functions = betterMysql.function;
// The functions are now in the "functions" variable!
```

## isArray

If you want to test if a object is a array, use this function. You don't have to use await and it returns a boolean \(true/false\).

{% code-tabs %}
{% code-tabs-item title="True" %}
```javascript
let array = ["Hi", "Bye"];
console.log(functions.isArray(array)); // Returns "true".
```
{% endcode-tabs-item %}

{% code-tabs-item title="False" %}
```javascript
let object = {hi: "goodbye"};
console.log(functions.isArray(object)); // Returns "false".
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## isClass

Now, if you want to test if a object is a class \(it can't be a object where the class constructor is already called\). You don't have to use await and it returns a boolean \(true/false\).

{% code-tabs %}
{% code-tabs-item title="True" %}
```javascript
let betterMysqlClientClass = require("better-mysql").client;
console.log(functions.isClass(betterMysqlClientClass)); // Returns "true".
```
{% endcode-tabs-item %}

{% code-tabs-item title="False" %}
```javascript
let betterMysqlClientClass = require("better-mysql").client;
let client = new betterMysqlClientClass({
    host: "db4free.net",
    user: "YOURUSERNAME",
    pass: "YOURPASSWORD123"
});
let object = {hi: "Bye"};

console.log(functions.isClass(client)); // Returns "false" because the class is already made.
console.log(functions.isClass(object)); // Returns "false" because it is a object and not a class.
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## isFunctionOfClass

If you want to to check if a object is a class, add this to every class.

{% code-tabs %}
{% code-tabs-item title="Only the one function" %}
```javascript
check() {
    return true;
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="The whole class" %}
```javascript
class example {
    constructor(options) {
        // Handle the constructor
    }
    check() {
        return true;
    }
    // The other class functions
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

