### リストインスタンスは半群なのよっ

　試しにもうひとつ、  
`Semigroup [a]`型と`(++)`演算子が半群であることを確認してみましょう。

```haskell
-- リストは半群である
instance Semigroup [a] where
  sappend = (++)

sgTestList :: IO ()
sgTestList = let sgLawAp' = sgLawAp :: [Float] -> [Float] -> [Float] -> Bool
             in quickCheck sgLawAp'
```
