---
description: 'How to make, load, chance and delete tables'
---

# Using tables

A MySQL database is constructed from tables. You can make, load, chance and delete tables, normally as many as you like!

If you want to work with tables, you have to load in a database. You can find more explanation for this at the [base &gt; Selecting a database](basis.md#selecting-a-database).

## See all the tables

If you want to see all the tables \(without the data in it\) you can use the function `database.getTables`. Here is a example.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let tables = await database.getTables();
console.log(tables); // Get a array with all the tables.
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.getTables().then(tables => {
    console.log(tables); // Get a array with all the tables.
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> To get the amount of tables there are in the database, log the length of `tables`.
>
> ```javascript
> console.log(tables.length); // Get a number of the amount of tables there are.
> ```

## Making a table

To make a table, use the `database.createTable` function. This is a example for making a table called `example` with the columns `name`, `mail` and `password`.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let table = await database.createTable("example", ["name", "mail", "password"]);
// Use the variable "table" for the table functions!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.createTable("example", ["name", "mail", "password"]).then(table => {
    // Use the variable "table" for the table functions!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Loading a table

If you want to load a table, use the function `database.loadTable`. This is a example for loading a table called `example`.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let table = await database.loadTable("example");
// Use the variable "table" for the table functions!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.loadTable("example").then(table => {
    // Use the variable "table" for the table functions!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Chancing a table

For chancing a table, you have to use the function `database.chanceTable`. Here you have to give up a action. Look at the different headings for all the actions.

### Rename a column

You can rename a column with the action name `rename_column`. Here is a example where the column `nname` will be renamed to `name` in the database `example`.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
await database.chanceTable("example", "rename_column", "nname", "name");
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.chanceTable("example", "rename_column", "nname", "name").then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Deleting a column

You can also delete a column with the action name `delete_column`. Here is a example where the column `hi` will be deleted of the database `example`.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
await database.chanceTable("example", "delete_column", "hi");
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.chanceTable("example", "delete_column", "hi").then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Clearing a table

If you want to reset all the data of a table, you can do that with the action `clear`. Here is a example where the table `example` will be cleared.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
await database.chanceTable("example", "clear");
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.chanceTable("example", "clear").then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Cloning a table

If you want to clone a table \(for a backup\), you can use the `clone` action. Here is a example where the table `example` will be cloned to `example2`.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
await database.chanceTable("example", "clone", "example2");
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.chanceTable("example", "clone", "example2").then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Deleting a table

If you want to delete a table, use the function `database.deleteTable`. Here is a example where the table `example` will get deleted.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
await database.deleteTable("example");
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
database.deleteTable("example").then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

