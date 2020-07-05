---
title: "Allow Only Numbers in Textbox"
date: 2020-07-05T14:44:50+01:00
draft: 
---

***

##### Allow only numbers in textbox 

```javascript
function allowOnlyNumbers(elementid){
  $("#" + elementid).getControl().keypress( function() {
    $(this).val($(this).val().replace(/[^\d].+/, ""));
        if ((event.which < 48 || event.which > 57)) {
          event.preventDefault();
        }
 
  }); 
}
```