---
description: >-
  Let's start with the real job! Get all the data, get some bits and sort the
  data!
---

# Getting data

## Get all the data

Let's start with getting all the data. If you want to get all the data, use the function `table.getAll`. There are no parameters that you have to use! Here is a example.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
let allTheDate = await table.getAll();
// Everything is now in the variable "allTheData"
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
table.getAll().then(() => {
    // Everything is now in the variable "allTheData"
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Getting specific data

You can also get specific data. For that, you can use the function `table.where`. You have to use a filter for the one parameters.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
// Making the filter
let filter = new client.filter(null, "and");
filter.add("mail", "@gmail.com", "ends");

// Getting the information from the database
let gmails = await table.where(filter);

// Everyone with a gmail address is now in the variable "gmails"!
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
// Making the filter
let filter = new client.filter(null);
filter.add("mail", "@gmail.com", "ends");

// Getting the information from the database
let gmails = table.where(filter).then(gmails => {
    // Everyone with a gmail address is now in the variable "gmails"!
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> For more explanation about filters, view the [using a filter](../util/using-a-filter.md) page.

## Sorting data

Let's say you have a point system in a Discord bot. And then you want to make a leader board. With Better-MySQL is that really simple! The only thing you have to do, is use the `table.sort` function and send the results.  
For the sorting function, you have to make a filter and give the column up that you want to sort. Here a example.

{% code-tabs %}
{% code-tabs-item title="Await example" %}
```javascript
// Making the filter. For the top 10 you only have to get 10 results.
let filter = new client.filter(10);

// Requesting
let leaderboard = await table.sort(["level", "points"], filter); // First sort on the level, then on the points

// Here you have to handle the sending.
```
{% endcode-tabs-item %}

{% code-tabs-item title=".then example" %}
```javascript
// Making the filter. For the top 10 you only have to get 10 results.
let filter = new client.filter(10);

// Requesting
table.sort(["level", "points"], filter).then(leaderboard => { // First sort on the level, then on the points
    // Here you have to handle the sending.
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}



