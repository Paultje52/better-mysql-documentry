---
description: Now let's set some data in to the database!
---

# Setting data

## Adding

First, let's start off with something simple! You have a database called `customers` with the columns `name, mail, ordersArray`. Now you want to add a customer. You can do that with the `table.add` function. Here are two examples.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
// First, let's make the array of the order.
let orders = [1, 5, 9];

// Now add it to the table.
await table.add(["Paul", "paul@example.mail", orders]);
// Done!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
// First, let's make the array of the order
let orders = [1, 5, 9];

// Now add it to the database
table.add(["Paul", "paul@example.mail", orders]).then(() => {
    // Done!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Updating

Now, the customer ordered product number three. Then you want to add that to the array. You can do that with the `table.update` function.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
// First, let's get the customer information
let filter = new client.filter(1)
filter.add("name", "Paul");
let customer = await table.where(filter);

// Now, get the array, add order number two and sort it (because we can)
let orderArray = customer.orderArray;
orderArray.push(2);
orderArray.sort();

// Now, let's update the database
await table.update(filter, {column: "ordersArray", value: orderArray});
// Array updated!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
// First, let's get the customer information
let filter = new client.filter(1)
filer.add("name", "Paul");
table.where(filter).then(customer => {
    // Now, get the array, add order number two and sort it (because we can)
    let orderArray = customer.orderArray;
    orderArray.push(2);
    orderArray.sort();
    
    // Now, let's update the database
    table.update(filter, {column: "ordersArray", value: orderArray}).then(() => {
        // Array updated!
    });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Ensure

If you want to add a row if something in it doesn't exists, you can do that with the `table.ensure` function. Here is a example.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let filter = new client.filter();
filter.add("name", "Jan");
let res = await table.ensure(filter, ["Paul", "paul@example.com", "password"]);
// Use the variable "res" with the data.
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
let filter = new client.filter();
filter.add("name", "Jan");
table.ensure(filter, ["Paul", "paul@example.com", "password"]).then(res => {
    // Use the variable "res" with the data.
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Deleting

Oke, finaly: deleting data! You can delete data with the `table.delete` function and a filter. Here a example.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let filter = new client.filter(1)
filter.add("name", "Paul");
await table.delete(filter);
// Row deleted!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
let filter = new client.filter(1)
filter.add("name", "Paul");
table.delete(filter).then(() => {
    // Row deleted!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

