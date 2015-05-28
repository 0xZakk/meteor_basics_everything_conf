===
# What is Meteor.js?

#### Zakk Fleischmann


===
# Introduction to Meteor
- http://mystical_mountain_fairies_of_vienna.meteor.com/a

===
# What is Meteor?
- Full stack framework (sort of like Rails but for JS)
- Single language run on both the client and the server

![image](http://joshowens.me/content/images/2015/May/all-the-stack.jpg)

Credit: Josh Owen

[demo to do list application]

===
# Reactivity

- In other JS frameworks, we would have to make ajax calls or use sprockets to keep our data up to date
- Meteor takes care of this for us through a reactive programming packaged, Tracker


In our template:

```
<template name="tasksList">
  <ul>
    {{#each tasks}}
      <li>{{task}}</li>
    {{/each}}
  </ul>
</template>
```

In our JS:

```
Template.tasksList.helpers({
  tasks: function() {
    return Tasks.find();
  }
});
```
===
# Meteor Collections

- Special data type that stores data on the server and synchronizes it on the browser in real time

```
Tasks = new Mongo.Collection('task');
```
- Exists on the server (database), with a subset of the data existing on the client in browser memory

===
# Publications and Subscriptions

- Publishing and Subscribing is how we coordinate what data gets saved in the client's memory (we 'publish' data and then 'subscribe' to it)

Publish:

```
  Meteor.publish("tasks", function () {
    return Tasks.find({
      $or: [
        { private: {$ne: true} },
        { owner: this.userId }
      ]
    });
  });
```

Subscribe:

```
  Meteor.subscribe("tasks");
```
===
# Why does any of this matter?
## Rails
- Think through Rails process: like a waiter at a restaurant

## Meteor
- More like a food truck





