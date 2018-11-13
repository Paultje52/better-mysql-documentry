---
description: >-
  You can use a filter for sorting data, search for specific data and update
  data!
---

# Using a filter

The filter class is an extender of the client. So you can make a filter by doing this.

```javascript
// Creating the filter
let filter = new client.filter();
```

## Constructor

In the constructor, you can give up the limit and the divide for each filter. More explanation for this can you find at [the limit section](using-a-filter.md#setting-the-limit) and [the divide section](using-a-filter.md#setting-the-divide-option).   
Here are some examples.

{% code-tabs %}
{% code-tabs-item title="Without data " %}
```javascript
// Creating the filter
let filter = new client.filter();
```
{% endcode-tabs-item %}

{% code-tabs-item title="With the limit" %}
```javascript
// Setting the limit to 10 in the constructor
let filter = new client.filter(10);
```
{% endcode-tabs-item %}

{% code-tabs-item title="With the limit and divide" %}
```javascript
/*
    Limit: 10
    Divide: or
*/
let filter = new client.filter(10, "or");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Setting the limit

If you are using `where` for example, you can say to the MySQL database: I only want 10 results.  
You can set this in the constructor or in the `filter.setLimit` function. An example to set the limit to 10.

```javascript
// Setting the limit to 10
filter.setLimit(10);
```

## Setting the divide option

In a filter you can set filters, like `name = "Paul"` and `mail includes ".nl"`. Those two filters has to be divided. And there comes the divide option.   
This you can use:  
`and`, so you say that the name has to be `Paul`AND the mail has to include `.nl`.  
`or`, then the name has to be `Paul`OR the mail has to include `.nl`.

Here is a example to set the divide \(`and` and `or` are fully written here\).

{% code-tabs %}
{% code-tabs-item title="And" %}
```javascript
// Setting the divide option to and
filter.setDivide("and");
```
{% endcode-tabs-item %}

{% code-tabs-item title="Or" %}
```javascript
// Setting the divide option to or
filter.setDivide("or");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Adding a filter

Now the main purpose for a filter: the filter itself. To add a filter, use the `filter.add` function. Here are some examples for filters.

{% code-tabs %}
{% code-tabs-item title="Equals" %}
```javascript
// The name has to be "Paul"
let filterThingOne = filter.add("name", "Paul"); // You don't have to give up the type, that is "equals" by default.
```
{% endcode-tabs-item %}

{% code-tabs-item title="Includes" %}
```javascript
// The mail has to includes ".nl"
let filterThingTwo = filter.add("mail", ".nl", "includes");
```
{% endcode-tabs-item %}

{% code-tabs-item title="Starts" %}
```javascript
// The name hase to starts with "a";
let filterThingThree = filter.add("name", "a", "starts");
```
{% endcode-tabs-item %}

{% code-tabs-item title="Ends" %}
```javascript
// The address has to end with a "g"
let filterThingFour = filter.add("address", "g", "ends");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

