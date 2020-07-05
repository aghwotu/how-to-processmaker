---
title: "Check if Texbox Is Equal"
date: 2020-07-05T14:41:10+01:00
draft: 
---

***

##### Check if the value of two textboxes are the same 

```javascript
function isSame(element1, element2) {
    let val1 = $("#" + element1).getValue();
    let val2 = $("#" + element2).getValue();
    return (val1 == val2);
}
```