## 群型クラスと群インスタンス

```haskell
-- 群型クラス
class Group a where
  gappend :: a -> a -> a
  gempty  :: a
  ginv    :: a -> a  -- inverse

-- 群インスタンスの例
instance Group Int where
  gappend = (+)
  gempty  = 0
  ginv    = negate
```

　ひとまず群型クラスとGroup Int型の定義のみを並べてみました。

群の満たす法則は
1. 結合律
2. 単位元律
3. 逆元の法則

でした。

それぞれ
1. `gappend`
2. `gempty`
3. `ginv`

が対応していて、Groupの`gappend`と`gempty`は  
このMonoidの`mappend`と`mempty`と同一のものです。[※1](#comment1)

そう、モノイド(`Monoid`)に逆元の存在(`ginv`)を足した構造が群でした！

- - -

<a name="comment1">※1</a>  
今回の群インスタンスの例は、半群, モノイドと違い
演算が`(+)`、単位元が`0`になっています。  
整数集合には`5`の逆元がないから、
`((*), 1)`は群にはなれないのです！  
(
```
5 * 0.2 = 0.2 * 5 = 1
```
にはなりますが、0.2は整数ではありません！  
)
