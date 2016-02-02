以下はMonoidインスタンスの例です。

MonoidTest.hs  
```haskell
import Test.QuickCheck

-- Monoidインスタンスの例
instance Monoid Int where
  mappend = (*)
  mempty  = 1

-- 結合律
mnLawAp :: (Monoid a, Eq a) => a -> a -> a -> Bool
mnLawAp x y z = (x `mappend` y) `mappend` z == x `mappend` (y `mappend` z)

-- 単位元律
mnLawEm :: (Monoid a, Eq a) => a -> Bool
mnLawEm x =
  let left  = mempty `mappend` x
      right = x `mappend` mempty
  in left == right && right == x

-- Monoid Intがモノイドであることのテスト ( 結合律に対する )
mnTestApInt :: IO ()
mnTestApInt = let mnLawAp' = mnLawAp :: Int -> Int -> Int -> Bool
              in quickCheck mnLawAp'

-- Monoid Intがモノイドであることのテスト ( 単位元律に対する )
mnTestEmInt :: IO ()
mnTestEmInt = let mnLawEm' = mnLawEm :: Int -> Bool
              in quickCheck mnLawEm'
```

