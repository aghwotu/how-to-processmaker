---
title: "Show Multiple Fields"
date: 2020-07-05T14:35:13+01:00
draft: 
---

***

##### Show multiple form fields

```javascript
//this accepts an array of textbox ids
function showMultipleElements(arrInput) {
    arrInput.forEach(showElementId); 
    function showElementId(item, index) {
      return $("#" + item ).show();
    }
}
```