---
title: "Hide Multiple Fields"
date: 2020-07-05T14:35:34+01:00
draft: 
---

***

##### Hide multiple form fields

```javascript
//this accepts an array of textbox ids
function hideMultipleElements(arrInput) {
    arrInput.forEach(hideElementId); 
    function hideElementId(item, index) {
      return $("#" + item ).hide();
    }
}
```