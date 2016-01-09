### 「以下の条件」について

> 結合律

> S の各元 a, b, c に対して、等式 (a • b) • c = a • (b • c) が満たされる。

これはtest1で確認していることで、  
「Semigroupインスタンスは必ずtest1テストを通します」  
と言っているのと同じことです。

ということでSemigroup Int型は半群である、ということになります。


試しにSemigroup [a]型と(++)演算子が半群であることを確認してみましょう。

```haskell
instance Semigroup [a] where
  sappend = (++)

sgTest2 :: IO ()
sgTest2 = let sgLaw' = sgLaw :: [Float] -> [Float] -> [Float] -> Bool
          in quickCheck sgLaw'
```
