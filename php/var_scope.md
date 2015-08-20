---
layout: default
---

# PHPではまりやすい変数のスコープ

## if, for ブロック

if, forのブロック内で宣言した変数は、そのブロックを出ても有効

```php
if($flag) {
    $hoge = 'Hello';
}

echo $hoge; //コンパイルエラーにはならない
// $flagがtrueならHelloだし、falseならnull
```


## グローバル変数と関数

```php
$a = 1;

  function fuga() {
    echo $a;
  }

  fuga(); // => null
```


globalの値を参照したい場合は


```php
$a = 1;

function fuga() {
    global $a
    echo $a; // => 1
    
    echo $GLOBALS['a']; // => 1
}
```

## クラス内のメソッド

```php
$a = 1;

class Hoge {
    function fuga() {
        global $a;
        echo $a
    }
}
```

これで `fuga()` を呼んでも `1` は出力されない！！

## autoloadでの変数スコープでハマる

## 参考

* http://php.net/manual/ja/language.variables.scope.php
