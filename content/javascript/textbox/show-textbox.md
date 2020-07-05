---
title: "Show Textbox"
date: 2020-07-05T14:34:06+01:00
draft: 
---

***

##### Show textbox

```javascript
function showElement(elementid, validate = "no") {
    if (validate == "yes") return $("#" + elementid).enableValidation().show();
    return $("#" + elementid).show();
}
```