---
layout: default
title: ブロック要素の高さをmiddleにする
---

# ブロック要素の高さをmiddleにする

## position: absolute 方式

```
<div class="parent">
  <div class="child">
    ほげええ
  </div>
</div>
```

```
.parent {
  position: relative;
  height: 30px;
}

.child {
  height: 20px;
  position: absolute;
  top: 50%;
  margin: -10px
}
```

## table-cell方式

```
<div class="parent">
  <div class="child">
    ほげええ
  </div>
</div>
```


```
.parent {
  display: table-cell;
  vertical-align: middle;
}
```
