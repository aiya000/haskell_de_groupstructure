以下はMonoidインスタンスの例です。

```haskell
import Test.QuickCheck

-- 結合律
mnLawAp :: (Monoid a, Eq a) => a -> a -> a -> Bool
mnLawAp x y z = (x `mappend` y) `mappend` z == x `mappend` (y `mappend` z)

-- 単位元律
mnLawEm :: (Monoid a, Eq a) => a -> Bool
mnLawEm x =
  let left  = mempty `mappend` x
      right = x `mappend` mempty
  in left == right && right == x

-- Monoidインスタンスの例
instance Monoid Int where
  mappend = (*)
  mempty  = 1

-- Monoid Intがモノイドであることのテスト ( 結合律に対する )
mnTestAp1 :: IO ()
mnTestAp1 = let mnLawAp' = mnLawAp :: Int -> Int -> Int -> Bool
            in quickCheck mnLawAp'

-- Monoid Intがモノイドであることのテスト ( 単位元律に対する )
mnTestEm1 :: IO ()
mnTestEm1 = let mnLawEm' = mnLawEm :: Int -> Bool
            in quickCheck mnLawEm'
```

