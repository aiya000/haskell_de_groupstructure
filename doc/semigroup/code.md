## 半群を表すHaskellのコード

以下は型クラス「半群」と、半群インスタンスの例です。

```haskell
import Test.QuickCheck

-- 半群型クラス
class Semigroup a where
  sappend :: a -> a -> a

-- 半群の満たすべき法則
sgLaw :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLaw x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)

-- 半群インスタンスの例
instance Semigroup Int where
  sappend = (*)

-- Semigroup Intが半群であることのテスト
sgTest1 :: IO ()
sgTest1 = let sgLaw' = sgLaw :: Int -> Int -> Int -> Bool  -- QuickCheckのために単相化
          in quickCheck sgLaw'
```
