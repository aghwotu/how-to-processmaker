---
title: "Enable Textbox Validation"
date: 2020-07-05T14:36:06+01:00
draft: 
---

***

##### Enable validation on textbox 

```javascript
function requireElement(elementid) {
    return $("#" + elementid).enableValidation();
}
```

{{% notice note %}}
You have to make the form control `required` in order to be able to enableValidation dynamically
{{% /notice %}}