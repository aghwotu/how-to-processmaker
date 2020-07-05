---
title: "Is Grid Column Empty?"
date: 2020-07-05T14:52:33+01:00
draft: 
# tags: ["processmaker", "grid"]
---


##### Check if a Grid column is empty

```javascript
function isGridColumnEmpty (gridId, rowNo, columnNo) {
  if (!($("#" + gridId).getValue(rowNo, columnNo) != '')) {
    return [false, columnNo];
  }
  return [true, columnNo];
}
```