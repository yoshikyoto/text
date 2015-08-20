---
layout: default
title: ブロック要素をセンタリングする
---

# ブロック要素をセンタリングする

以下のようなhtmlがあったとする

```
<div class="parent">
    <div class="center-children">
        まんなかにしたい
    </div>
</div>
```

この `div.center-children` をセンタリングするには、以下の2つをすればよい。

* `div.parent` 部分の幅を決めてあげる
* `div.center-children` 部分の左右の `margin` を `auto` にする

例

```
.parent {
    width: 800px;
}

.center-children {
    margin: 0px auto;
}
```

## text-align, vertical-align について

* `text-align`
* `vertical-align`

はインライン要素を含むブロック要素に指定することで、中に含まれるインライン要素がセンタリングされる。
ブロック要素はセンタリングされない。
また、いずれにせよブロック要素のサイズが決まっていないとセンタリングされない。

* 参考: [インライン要素を左寄せ・中央寄せ・右寄せする方法 ](http://www.acky.info/tips/css/00001.html)
