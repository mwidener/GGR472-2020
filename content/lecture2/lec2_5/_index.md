---
title: "Spatial Data for the Web"
date: 2020-01-03T15:16:16-05:00
chapter: true
weight: 5
---

#### Other formats more common in web world
Many other, compact data structures that work better for online transmission/compression

One major format is based off of markup languages.

* What is XML?
  * Extensible Markup Language
  * Store/transport data
  * Human and machine readable
* XML doesn’t do anything
  * Information wrapped in tags
  * XML carries data, HTML designed to display data
  * XML doesn’t have predefined tags (e.g. <p>), HTML does

#### XML Example:
``` xml
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```
A computer program reads the tags and displays the text based on predefined rules

## NOTE
##### To: Tove
##### From: Jani
#### Reminder
##### _Don't forget about the milk!_
