## 半群を表すHaskellのコード

以下は型クラス「半群」と、半群インスタンスの例です。

Semigroup.hs  
```haskell
module Semigroup
  ( Semigroup
  , sappend
  , sgLawAp
  ) where

-- 半群型クラス
class Semigroup a where
  sappend :: a -> a -> a

-- 半群の満たすべき法則 ( 結合律 )
sgLawAp :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLawAp x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)
```

SemigroupTest.hs  
```haskell
-- 半群インスタンスの例
instance Semigroup Int where
  sappend = (*)

-- Semigroup Intが半群であることのテスト
sgTestAp :: IO ()
sgTestAp = let sgLawAp' = sgLawAp :: Int -> Int -> Int -> Bool  -- QuickCheckのために単相化
           in quickCheck sgLawAp'
```
