---
title: "Hide Grid Column"
date: 2020-07-05T14:47:14+01:00
draft: 
---

***

##### Hide a grid column

```javascript
function hideGridColumn(gridId, index) {
    $("#" + gridId).hideColumn(index);
    $("#" + gridId).disableValidation(index);
}
```