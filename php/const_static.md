---
layouts: default
---

# PHPでconstとstatic変数の呼び出し方の違いでハマった

## const

定義の時

```
class Constants {
    const CONST_NUM = 1;
}
```

呼ぶ時

```
echo Constants::CONST_NUM;
```

注意

* $は使わない


## static

定義の時

```
class Sample {
    static $value = 5
}
```

呼び出しの時

```
scho Sample::$value;
```

注意

* $が必要
* $がちょっとだけ変なところにくっつく
