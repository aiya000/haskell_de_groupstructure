## リストインスタンスはモノイドでもあるのよ

　モノイドでももうひとつ、`Monoid [a]`型と`(++)`演算子がモノイドであることを確認してみます。

といっても実は`Monoid [a]`は`GHC.Base`にて定義されているので、テストのみ行ってみます。

```haskell
mnTestApList :: IO ()
mnTestApList = let mnLawAp' = mnLawAp :: [Float] -> [Float] -> [Float] -> Bool
               in quickCheck mnLawAp'

mnTestEmList :: IO ()
mnTestEmList = let mnLawEm' = mnLawEm :: [Float] -> Bool
               in quickCheck mnLawEm'
```

OK、通りました。

- - -

仮想的に、`Monoid [a]`を書くとすれば、以下のようになるでしょう。

```haskell
instance Monoid [a] where
  mappend = (++)
  mempty  = []
```
