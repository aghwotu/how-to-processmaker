---
title: "Disable Grid"
date: 2020-07-05T14:28:04+01:00
draft: 
---

***

##### Disable a grid

```javascript
function disableGrid(elementid) {
  return $("#" + elementid).find("input,button,textarea,select").attr("disabled", true);
}
```