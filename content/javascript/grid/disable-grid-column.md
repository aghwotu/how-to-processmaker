---
title: "Disable Grid Column"
date: 2020-07-05T14:55:11+01:00
draft: 
---

##### Disable a grid column

```javascript
function disableGridColumn(gridId, gridColumnId) {
  let gridRows = $("#" + gridId).getNumberRows();
  
    for (i = 1; i <= gridRows; i++) {
        $("#form\\[" + gridId + "\\]\\[" +i+ "\\]\\[" + gridColumnId + "\\]").attr("disabled", true);
        
    }

}
```