## 半群を表すHaskellのコード

以下は型クラス「半群」と、半群インスタンスの例です。

```haskell
import Test.QuickCheck

class Semigroup a where
  sappend :: a -> a -> a

sgLaw :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLaw x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)

instance Semigroup Int where
  sappend = (*)

-- Test
sgTest1 :: IO ()
sgTest1 = let sgLaw' = sgLaw :: Int -> Int -> Int -> Bool  -- QuickCheckのために単相化
          in quickCheck sgLaw'
```
