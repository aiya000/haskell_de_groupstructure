### リストインスタンスは半群なのよっ

試しにもうひとつ、  
Semigroup [a]型と(++)演算子が半群であることを確認してみましょう。

```haskell
instance Semigroup [a] where
  sappend = (++)

sgTest2 :: IO ()
sgTest2 = let sgLaw' = sgLaw :: [Float] -> [Float] -> [Float] -> Bool
          in quickCheck sgLaw'
```
