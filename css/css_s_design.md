---
layout: default
title: CSS設計の教科書メモ
---

# CSS設計の教科書メモ

## idとかよりもclassを使う

* idセレクタは優先度が高め
* idを使うのはheaderとfotterくらいの方が良い

## セレクタがHTMLに依存しないようにする

* セレクタにdom名は使わない
* ネストは使わない

### OK

```
<section class="content">
  <h1 class="content-title">
    title
  </h1>
</section>
```

```
.content {
  width: 600;
}

.content-title {
  font-size: 1.5em;
}
```

### NG

* h1が何らかの理由でh2に変更されたらcssにも対応が必要
* `.content` セレクタの名前が変わったりしたら全部変えなきゃいけない
* 何らかの理由で `h1` が `.content` の外側に配置されることになったらcssも変更しなければならない
* `.content-title h1` だけ別の部分で再利用したりできない

```
<section class="content">
  <h1>
    title
  </h1>
</section>
```

```
.content {
  width: 600;
}

.content h1 {
  font-size: 1.5em;
}
```

## 共通部分をくくりだして再利用性を上げる

### OK

```
<header>
  <img class="logo">
</header>
<footer>
  <img class="logo logo-small">
</footer>
```

### NG

* 共通部分を変更しようと思ったら両方変えないといけない
* メニューにロゴを追加したい、となった場合に使い回しが効かない

```
<header>
  <img class="logo">
</header>
<footer>
  <img class="logo-footer">
</footer>
```
