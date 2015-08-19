---
layout: default
---

# PHPではまりやすい変数のスコープ

## if, for ブロック

if, forのブロック内で宣言した変数は、そのブロックを出ても有効


```

if($flag) {
    $hoge = 'Hello';
}

echo $hoge; //コンパイルエラーにはならない
// $flagがtrueならHelloだし、falseならnull

```


## グローバル変数と関数


```

$a = 1;

function fuga() {
    echo $a;
}

fuga(); // => null

```


globalの値を参照したい場合は


```

$a = 1;

function fuga() {
    global $a
    echo $a; // => 1
    
    echo $GLOBALS['a']; // => 1
}

```


## 参考

* http://php.net/manual/ja/language.variables.scope.php
