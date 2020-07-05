---
title: "Empty Textbox"
date: 2020-07-05T14:32:42+01:00
draft: 
---

***


##### Empty a textbox field

```javascript
function setEmpty(elementid) {
  return $("#" + elementid).setValue('');
}
```