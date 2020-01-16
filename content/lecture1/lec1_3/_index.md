---
title: "Basic Programming Concepts"
date: 2020-01-03T15:17:31-05:00
chapter: true
weight: 3
---
# Basic Programming Concepts

## Variable assignment

```JS
  var x = 12
  var blah = "some text that i'm writing right now!"
  blah = x
  y = blah - x
```

## Arrays
```JS
var universities = ["UofT", "Western", "McMaster"];
universities[0] //will return "UofT"
```

## Conditional statements
```JS
if (condition) {
  //  block of code to be executed if the condition is true
}
```
An example from https://www.w3schools.com/js/js_if_else.asp
```JS
if (hour < 18) {
  greeting = "Good day";
}
else {
  greeting = "Good evening"
}
```
What would this return now?


## Loops

```JS
var i;
for (i = 0; i < universities.length; i++) {
  text += universities[i] + "<br>";
}

/*will print:
 UofT
 Western
 McMaster
 */
```

## To the board!

![let's go](https://media.giphy.com/media/XoW4aVP3LhBaoB7FuJ/giphy.gif)
