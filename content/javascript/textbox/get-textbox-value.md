---
title: "Get Textbox Value"
date: 2020-07-05T14:42:07+01:00
draft: 
---

***

##### Get the value of a textbox 

```javascript
function fetchValue(elementid) {
    return $("#" + elementid).getValue();
}
```