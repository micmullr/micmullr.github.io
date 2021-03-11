---
title: 'Hallo'
date: 2021-03-10
permalink: /posts/2012/08/blog-post-5/
tags:
  - cool posts
  - category1
  - category2
---



# Hallo 

Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!



https://support.typora.io/Draw-Diagrams-With-Markdown/



~~~gfm
```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```
~~~


```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

```flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end

st->op->cond
cond(yes)->e
cond(no)->op
```
<div id="diagram"></div>
<script>
  var diagram = flowchart.parse("the code definition");
  diagram.drawSVG('diagram');

  // you can also try to pass options:

  diagram.drawSVG('diagram', {
                              'x': 0,
                              'y': 0,
                              'line-width': 3,
                              'line-length': 50,
                              'text-margin': 10,
                              'font-size': 14,
                              'font-color': 'black',
                              'line-color': 'black',
                              'element-color': 'black',
                              'fill': 'white',
                              'yes-text': 'yes',
                              'no-text': 'no',
                              'arrow-end': 'block',
                              'scale': 1,
                              // style symbol types
                              'symbols': {
                                'start': {
                                  'font-color': 'red',
                                  'element-color': 'green',
                                  'fill': 'yellow'
                                },
                                'end':{
                                  'class': 'end-element'
                                }
                              },
                              // even flowstate support ;-)
                              'flowstate' : {
                                'past' : { 'fill' : '#CCCCCC', 'font-size' : 12},
                                'current' : {'fill' : 'yellow', 'font-color' : 'red', 'font-weight' : 'bold'},
                                'future' : { 'fill' : '#FFFF99'},
                                'request' : { 'fill' : 'blue'},
                                'invalid': {'fill' : '#444444'},
                                'approved' : { 'fill' : '#58C4A3', 'font-size' : 12, 'yes-text' : 'APPROVED', 'no-text' : 'n/a' },
                                'rejected' : { 'fill' : '#C45879', 'font-size' : 12, 'yes-text' : 'n/a', 'no-text' : 'REJECTED' }
                              }
                            });
</script>