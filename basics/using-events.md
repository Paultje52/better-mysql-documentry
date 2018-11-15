---
description: EVENTS!
---

# Using events

There are different events that you can use with better-MySQL.   
Now there is `1` event. Later, there will be more events.  
A events is a function that will be called when there happens something. If you want to make a event, use this code.

```javascript
client.on("EVENT", (eventDetails) => {
    // Handle the event.
});
```

## sql

The first event is when there will be send something to the MySQL server. The name of this event is `sql` and it has three or four parameters.  Here is a example.

```javascript
client.on("sql", (sql, place, func, placeInFunction) => {
    if (placeInFunction) func = `${func}.${placeInFunction}`;
    console.log(`Just runned ${sql} at ${place} in the function ${func}!`);
});
```

