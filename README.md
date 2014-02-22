repeatable
==========

Repeatable "template-less" jQuery plugin 

# Introduction

The Repeatable is template-less mechanism for populating various list, tables, etc. by arrays containing objects.
Temlate-less here means that you don't need to use templates for your repeteables anywere except of markup itself.

# Example

Let's assume that you would want to populate (render) some list with some data stored as objects in some array:

```javascript
var data = [
       { name: "Olga", age: 20, email: "aaa@example.com" },
       { name: "Peter", age: 30, email: "bbb@example.com" },
       { name: "Ivan", age: 15, email: "ccc@example.com" },
    ];
```

Then with the Repeatable you can define your list in markup as: 

```html
<ul id="people">
    <li><a href="mailto:{{this.email}}">{{this.name}}</a> <b if="this.age > 18">18+</b> </li> 
    <li>No data available</li>
</ul>
```

First `<li>` above is so called record template - it will appear in the DOM for each element in the data array. Second `<li>` element will appear once and only if you will feed the repeatable by empty array.

Having all these the Repeatable makes list population extremely simple:

```javascript
var list = $("ul#people").repeatable(); // declaring the repeatable
    list.value = data; // that's data population, sic!
```

Note `list.value = data;` above, by assigning array data to the value property of the repetable you are populating the list by the data.


Live demo: http://terrainformatica.com/widgets.js/repeatable/repeatable-test.htm

# Record template microformat

Any text or attribute value in the repeatable section may contain expressions enclosed in "mustache" brackets `{{ ...expr ...}}`. 

While populating records each such expression will be executed and it's return value (string) will be put in the DOM replacing `{{...}}` placeholder as a whole. 

## Environment variables

In repeatable expressions following variables have special meaning:

* `this` - refers to the record (object) being processed (rendered);
* `$index` - number, index of current record;
* `$first` - `true` if this is the first record;
* `$last` - `true` if this is the last record;
* `$length` - number, total number of records in the array.

## Conditionals

Any element inside repeatable section can be declared as conditional by using `if="...expr..."` attribute. Expression defined by the attribute will be evaluated and if its result is "truthy" the element will be rendered, otherwise - removed from the DOM.

