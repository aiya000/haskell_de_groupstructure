## モノイドを表すHaskellのコード

　モノイドは`Data.Monoid`にて、以下のように定義されています。  
なので自分で定義する必要はありません。 ﾔｯﾀｰ。

```haskell
-- モノイド型クラス
class Monoid a where
  mappend :: a -> a -> a
  mempty  :: a
```

`mappend`については我らの知る通り、半群の`sappend`と全く同じものです。  

```haskell
-- 半群型クラス
class Semigroup a where
  sappend :: a -> a -> a
```

そう、モノイドは半群の「二項演算」を持っているのでした。
( モノイドは、半群を拡張した構造でした )

加えて、`mempty`という定数が存在しています。  
では、もう一度`Int`を使って`Monoid Int`型を定義してみます。
