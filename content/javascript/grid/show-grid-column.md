---
title: "Show Grid Column"
date: 2020-07-05T14:47:33+01:00
draft: 
---

***

##### Show a grid column

```javascript
function showGridColumn(gridId, index) {
    $("#" + gridId).showColumn(index);
    $("#" + gridId).enableValidation(index);
}
```