---
title: "Check if Empty"
date: 2020-07-05T14:33:37+01:00
draft: 
---

***

##### Check if a form field is empty

```javascript
function isEmpty(elementid) {
    if($("#" + elementid).getValue() == '' ) return true;
    return false;
  
}
```