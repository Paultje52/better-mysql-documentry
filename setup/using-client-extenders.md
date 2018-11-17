---
description: Now easier that ever!
---

# Using client extenders

## Enabling client extenders

If you want to enable a client extender, you have to `use` it. You can do that on `the index`, `databases` and `tables`.   
If you go to the group `client extenders` in the right navigation, you can see all the client extenders that exits. Every page is a other extender. At the start of each client extender, you can see where to use it, for example: You can use the `getset` extender only in databases.

All the client extenders are in the object `client.extenders`. For example, you can asses the `getset` client extender with `client.extenders.getset`. 

Here is a example for enabling a client extender.

```javascript
let extenders = client.extenders;
// The getset client extender: you can only use it in the database.
let getset = databasse.use(extenders.getset);
let example = new getset("tableName");
```

## Making your own client extender

You can also make your own client extender! There are a couple steps before you can make your own!

### Stap one

First, think if you can do the basics of _better-MySQL_ and maybe a extender. You can, for example, practice by making an example for yourself. 

> If you made a example, what you think is very good, send me a message on Discord \(`Paultje#0933`\) or make a issue at [the GitHub project](https://github.com/Paultje52/better-mysql).

### Stap two

Next, look if the extender or some parts already exists in better-MySQL or a extender. If don't, make a plan and send me a message on Discord \(`Paultje#0933`\) or make a issue at [the GitHub project](https://github.com/Paultje52/better-mysql).

### Stap three

If I say that your idea is good, you can start with it! You start with the basics.

```javascript
module.exports = function(baseObject, place) {
    // The baseObject is the standard object of better-mysql, from the place where it is called.
    // The place is a string, where the extender is called. For example: "index", "database" or "table".
}
```

Let's say, you want to make a ensure method \(I know that this method already exists, but this is only a example!\). You can only use this extender in a table. So you set a `if` statement, where you check if the place is a table.

```javascript
if (place !== "table") throw "You can only use my in a table!";
```

Now you did this, you can start with your function\(s\). You can use a class \(what `getset` does\), or you can export a single function. However: you have to return it. So here are two examples of how you have to return it.

{% code-tabs %}
{% code-tabs-item title="Returning a single function" %}
```javascript
return function(PARAMS) {
    // Do something, like eating a pizza
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Returning a class" %}
```javascript
return class {
    constructor() {
        // Something new, again!
    }
    
    eat(something) {
        // Now, let's eat something!
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now, we are going to write the extender. This is a single function, so we are using the `returning a single function`.

For our ensure method, we have to use the params `key` and `value`. And, because we are lazy, we are going to use the ensure method that already exists. We have to use the filter class, so we require that at the top of our code.   
So, here is the completed code.

```javascript
const Filter = require("../filter.js");
module.exports = function(baseObject, place) {
    if (place !== "table") throw "You can only use my in a table!";
    return function(key, value) {
        if (!key) throw "No key to search for!";
        if (!value) throw "No value!";
        return new Promise(async (resolve, reject) => {
            let filter = new Filter();
            filter.add(key.column, key.keyword);
            resolve(await baseObject.ensure(filter, value));
        });
    }
}
```

### Stap four

When you finisht your code, and test it, you can send it to me via Discord \(`Paultje#0933`\) or make a issue at [the GitHub project](https://github.com/Paultje52/better-mysql).

### Stap five

And now the last stap: Wait until the next release, and then your extender is published. I write the documentary for your extender. You will get credits there, with your `github username` and/or your `discord`. 

