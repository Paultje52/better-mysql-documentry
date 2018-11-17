---
description: >-
  Getset is made by Paultje#0933 (327462385361092621) on Discord and Paultje52
  on GitHub > Paul also created the hole package.
---

# Getset

## Importing

First, let's import `getset`! You have to import it in a database, and the return is a class. In that class you can load or create a table, to use `getset`! 

> If you are using a existing table, the table can only have the column `k` and `v`. Nothing more.

```javascript
// Loading the client.
let client = new betterMysql({
  host: "HOST",
  user: "USERNAME",
  pass: "PASSWORD"
});
// Loading the database
client.loadDatabase("DATABASE").then(async (database) => {
  // Importing getset
  let getSet = database.use(client.extenders.getset);
  // Making/loading a table
  let example = new getSet("example");
});
```

You have two parameters in the constructor.  
- The table name: Required. The name of the table.  
- Loading in the memory: Optional, by default `true`. Loading everything in the memory.

> If you have loading in the memory enabled, you don't have to use await. Everything will be saved to a variable, and then everything in the server will be updated. This is really fast.
>
> If you set the loading in memory to `false`, you can use the same functions, but then with await. Everything will be requested at the server. Usually, this is slower.

## waitForReady

If you are using the loading in memory, you have to wait until everything is loaded before you can start. Usually, this takes about 5 seconds. This is a `await` function, so you can set this in your code.

```javascript
await example.waitForReady();
// Ready!
```

There are two variables that are working with this: `example.readyState` and `example.ready`.   
ReadyState is a string, `ready` or `not ready`.  
Ready is a boolean, `true` or `false`.

## get\(key, path\)

Next, getting data!  
The `key` is always required, but the `path` only if you are using objects AND if you have `loading in memory` at `false`.  
Here is a example.

{% code-tabs %}
{% code-tabs-item title="Loading in memory enabled" %}
```javascript
let result = example.get("result"); // "Result!"
let json = example.get("json"); // "{a: "b", c: ["d", "e", "f"]}"
let jsonObject = example.get("json.a") // "b"
```
{% endcode-tabs-item %}

{% code-tabs-item title="Loading in memory disabled" %}
```javascript
let result = example.get("result"); // "Result!"
let json = example.get("json"); // "{a: "b", c: ["d", "e", "f"]}"
let jsonObject = example.get("json", "a") // "b"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## set\(key, value, path\)

Now, let's set some data! Just like the get function, you can use the `path`, if you have `loading in memory` at `true` and you are setting something in a already existing object.  
Here is a example, again!

{% code-tabs %}
{% code-tabs-item title="Loading in memory enabled" %}
```javascript
example.set("number", 123); // "123"
example.set("json.g", "h"); // "{a: "b", c: ["d", "e", "f"], g: "h"}"
```
{% endcode-tabs-item %}

{% code-tabs-item title="Loading in memory disabled" %}
```javascript
example.set("number", 123); // "123"
example.set("json", "h", "g"); // "{a: "b", c: ["d", "e", "f"], g: "h"}"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Delete\(key, path\)

And now, the last one! Path, you know it.  
And example.

{% code-tabs %}
{% code-tabs-item title="Loading in memory enabled" %}
```javascript
example.delete("number"); // "undefined"
example.delete("json.g"); // "{a: "b", c: ["d", "e", "f"]}"
```
{% endcode-tabs-item %}

{% code-tabs-item title="Loading in memory disabled" %}
```javascript
example.delete("number"); // "undefined"
example.delete("json", "g"); // "{a: "b", c: ["d", "e", "f"]}"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Later

Later, there will be more functions!



