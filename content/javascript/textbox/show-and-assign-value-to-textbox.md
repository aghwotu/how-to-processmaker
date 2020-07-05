---
title: "Show and Assign to Textbox"
date: 2020-07-05T14:37:43+01:00
draft: 
---

***

##### Show and assign a value to a textbox 

```javascript
function showandAssignValue(element, value) {
    return $('#' + element).show().setValue(value);
}
```