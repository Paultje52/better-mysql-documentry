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

> If you want unlimited results, you can do that by giving up the value `0` or `null`.

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

{% code-tabs-item title="Less" %}
```javascript
// If the address_number is less then "5"
let filterThingFive = filter.add("address_number", 5, "less");
```
{% endcode-tabs-item %}

{% code-tabs-item title="Greater" %}
```javascript
// If the address_number is greater then "50"
let filterThingSix = filter.add("address_number", 50, "greater");
```
{% endcode-tabs-item %}

{% code-tabs-item title="Between" %}
```javascript
// If the rating is between "6" and "10"
let filterThingSeven = filter.add("rating", [6, 10], "between");
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> Warning!   
> - If you are using `less`, `greater` or `between` the column and keyword has to be a number!  
> - If you are using `between`, the keyword has to be a array of TWO numbers!

## Editing a filter

You can edit a filter with the `filter.chance` function. If you want to chance a filter, you have to get the ID of the filter. Each filter that you add has a ID, starting by one and counting up. So if you want to chance the second filter that you added, the ID is two.   
But, you can also save the filter object in a variable, like all the examples of [adding a filter](using-a-filter.md#adding-a-filter). Then the ID is `<VARIABLE>.id`. Here are some examples.

{% code-tabs %}
{% code-tabs-item title="With variable" %}
```javascript
// Making the filter, the name has to be "Paul".
let filterThing = filter.add("name", "Paul");

// Now we are chancing the filter so the name has to INCLUDE "Paultje".
filter.chance(filterThing.id, {type: "includes", keyword: "Paultje"});
```
{% endcode-tabs-item %}

{% code-tabs-item title="Without variable" %}
```javascript
// Making the filter: address has to include "b"
filter.add("address", "b", "includes"); // Filter three

// Editing the filter: address has to include "a"
filter.chance(3, {keyword: "a"});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Using the filter

If you have made your filter, you can use it for different functions. The only thing you have to do is giving the filter class up in to the object. _Better-MySQL_ will do the rest!

## Self writing a object \(advanced\)

If you want to write the object itself instead of using the filter, you can do that. If you have a filter, log the `filter.handle` function in the console, like this. Click on `Output` for the output.

{% code-tabs %}
{% code-tabs-item title="Input" %}
```javascript
// Making the filter
let filter = new client.filter(1, "or");
// Adding a filter
filter.add("name", "Paul", "includes");

// Logging the handle function
console.log(filter.handle());
```
{% endcode-tabs-item %}

{% code-tabs-item title="Output" %}
```javascript
{ limit: 1,
  divide: 'OR',
  filters: [ { column: 'name', keyword: 'Paul', type: 'includes' } ] }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Here you can see the object that will be translated directly to SQL and then requested. If you want, you can   make this object for yourself. Just remember:

* The limit has to be a number.
* The divide has to be in capital letters, `AND` or `OR`.
* The filters is a array with objects in it.
  * A filter object has to includes `column`, `keyword` and `type`.

    * The column has to be a string: This column has to exists in the table!
    * The keyword has to be a string or array: This can be what you want!

    > WARNING: Only if the type is `between` the keyword can be a array with two numbers, otherwise it has to be a string or number!

    * The type has to be a string: `equals`, `includes`, `starts`, `ends`, `less`, `greater` or `between`.

> I don't recommencement to use a object, but if you really want, you can.

