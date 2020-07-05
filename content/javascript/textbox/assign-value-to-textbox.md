---
title: "Assign Value to Textbox"
date: 2020-07-05T14:38:43+01:00
draft: 
---

***

##### Assign a value to a textbox 

```javascript
function assignValue(elementid, value) {
    return $("#" + elementid).setValue(value);
}
```