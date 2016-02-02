### Semigroupインスタンスが半群である条件について

最後に、半群の性質を見ていきます。

> 結合律  
> S の各元 a, b, c に対して、等式 (a • b) • c = a • (b • c) が満たされる。

これは`sgLawAp`が示していることと等価です。

```haskell
-- 半群の満たすべき法則
-- (x • y) • z = x • (y • z)
sgLawAp :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLawAp x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)
```

また以下で`QuickCheck`により、`Semigroup Int`が半群であることをテストしています。  

```haskell
-- Semigroup Intが半群であることのテスト
sgTestInt :: IO ()
sgTestInt = let sgLawAp' = sgLawAp :: Int -> Int -> Int -> Bool
            in quickCheck sgLawAp'
```

上記テストは正常に通ります。  
ということで`Semigroup Int`型は半群である、ということになります。
