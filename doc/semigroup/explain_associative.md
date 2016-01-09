### Semigroupインスタンスが半群である条件について

最後に、半群の性質を見ていきます。

> 結合律  
> S の各元 a, b, c に対して、等式 (a • b) • c = a • (b • c) が満たされる。

これはsgLawが示していることと等価です。

```
-- 半群の満たすべき法則
sgLaw :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLaw x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)
```

また、以下でSemigroup Intが半群であることをテストしています。  
( QuickCheck )

```
-- Semigroup Intが半群であることのテスト
sgTest1 :: IO ()
sgTest1 = let sgLaw' = sgLaw :: Int -> Int -> Int -> Bool  -- QuickCheckのために単相化
          in quickCheck sgLaw'
```

上記テストは正常に通ります。  
ということでSemigroup Int型は半群である、ということになります。
