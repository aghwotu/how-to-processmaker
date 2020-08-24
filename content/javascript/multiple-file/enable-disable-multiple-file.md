---
title: "Enable Disable Multiple File"
date: 2020-08-24T16:27:34+01:00
draft: 
---

***

##### Disable Multiple File

```javascript
function disableMultipleFile(multipleFileId) {

    let multipleFile = document.querySelector('#'+ multipleFileId +' button');
  
    multipleFile.classList.remove('btn-uploadfile');
    multipleFile.classList.add('btn-uploadfile-disabled');
}
```

***

##### Enable Multiple File

```javascript
function enableMultipleFile(multipleFileId) {

    let multipleFile = document.querySelector('#'+ multipleFileId +' button');
  
    multipleFile.classList.remove('btn-uploadfile-disabled');
    multipleFile.classList.add('btn-uploadfile');
}
```