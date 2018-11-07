---
description: The best place to start!
---

# Basis

## Installing better-mysql

First, we need to install better-mysql. This is not that hard.  
You need NodeJS, you can download that [here](https://nodejs.org/en/).

If you have NodeJS \(and NPM, this will be in the installation\), run this command at your projectfolder:

```javascript
npm i -s better-mysql
```

## Logging in to the account

Next, we have to login to the account of the mysql databases. Do that with the **host**, **username** and **password**. 

> For all the examples we use [db4free.net](https://db4free.net). As they website says: This is experimental. **So, don't use it for real projects!**

Make a file in your projectfolder with the extention .js, like _bot.js_, _server.js_ or _index.js_.

```javascript
const mysql = require("better-mysql");
let client = new mysql.client({
    host: "db4free.net",
    user: "YOURUSERNAME",
    pass: "YOURPASSWORD123"
)};
```

Let's look at the code:  
**In the first line** we load the module and set it in a contant variable called `mysql`. A constant variable can't be chanced, so it can't do any harm later.  
  
**In line two** we make the client. The module returns a object. Later the mysql server will also be in there, but for now you only have the client.   
The client is a class. That means that you can have more mysql connections at the same time. Each connection doesn't interfere with a other **and** all the instances haves the same functions. The functions are on the variabel `client`.   
  
**In line three** we give up the host. This chould be a string. This example is with [db4free.net](https://db4free.net).   
**In line four** we give up the username. You can use `user` and `username`and it chould be a string.  
**In line five** we give up the password. You can use `pass`and `password`and it chould be a string.  
**And line six** is just a end of the start.

## See the databases

To make/connect to a table, we have to use a database. But it can come in handy if you want to see the databases before we connect to a database. That can be done by those two lines of code:

{% code-tabs %}
{% code-tabs-item title="Main example" %}
```javascript
let databases = await client.getDatabases();
console.log(databases);
```
{% endcode-tabs-item %}

{% code-tabs-item title="Compact" %}
```javascript
console.log(await client.getDatabases());
```
{% endcode-tabs-item %}
{% endcode-tabs %}



As you can see, there are two examples: The `main example` and the `compact` example. The two examples uses the same code and calling the same function.

**But** the main example is storing the databases in a variable and then logging the variable, and the compact example is logging the return of the function.

> Both examples are using async and await, becouse we have to get a connection to the database. But, if you don't want to or don't know how to use async, you can also use .then!   
> **Here is a example of using .then.**
>
> ```javascript
> client.getDatabases().then(databases => {
>     console.log(databases);
> });
> ```

## Selecting a database

Now, let's select a database!

### Making a database

With better-mysql, you can make a database very simple. We are going to create a database called `example` . There are two ways, with await and with .then.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let database = await client.createDatabase("example");
// Use the variable "database" for using/creating a table.
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
client.createDatabase("example").then(database => {
    // Use the variable "database" for using/creating a table.
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Loading a database

If you already have a database, you can load it, so you can make/use tables! The database we are going to load is called `example`. There are two ways, with await and with .then.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let database = await client.loadDatabase("example");
// Use the variable "database" for using/creating a table.
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
client.loadDatabase("example").then(database => {
    // Use the variable "database" for using/creating a table.
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}



> If you have the database, you can go to [using tables](using-tables.md).



