---
title: "Enable Grid Column"
date: 2020-07-05T14:54:29+01:00
draft: 
---

##### Enable a grid column

```javascript
function enableGridColumn(gridId, gridColumnId) {
  let gridRows = $("#" + gridId).getNumberRows();
  
    for (i = 1; i <= gridRows; i++) {

        $("#form\\[" + gridId + "\\]\\[" +i+ "\\]\\[" + gridColumnId + "\\]").attr("disabled", false);
        
    }

}
```

```javascript
function enableGridColumn(gridId, gridColumnId) {
  let numberOfGrid = $("#" + gridId).getNumberRows();
  
  for (let index = 1; index <= numberOfGrid; index++) { 

      $("#" + gridId).find("#"+ gridId +"-body").find("#form\\["+ gridId +"\\]\\[" + index + "\\]\\["+ gridColumnId +"\\]").prop("disabled", false);
  }
}
```