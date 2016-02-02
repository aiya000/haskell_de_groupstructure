## 群を表すHaskellのコード

Group.hs  
```haskell
module Group
  ( Group
  , gappend
  , gempty
  , ginv
  , grpLawAp
  , grpLawEm
  , grpLawInv
  ) where

-- 群型クラス
class Group a where
  gappend :: a -> a -> a
  gempty  :: a
  ginv    :: a -> a  -- inverse

-- 結合律
grpLawAp :: (Group a, Eq a) => a -> a -> a -> Bool
grpLawAp x y z = (x `gappend` y) `gappend` z == x `gappend` (y `gappend` z)

-- 単位元律
grpLawEm :: (Group a, Eq a) => a -> Bool
grpLawEm x =
  let left  = gempty `gappend` x
      right = x `gappend` gempty
  in left == right && right == x

-- 逆元の存在
grpLawInv :: (Group a, Eq a) => a -> Bool
grpLawInv x =
  let left  = x `gappend` (ginv x)
      right = (ginv x) `gappend` x
  in left == right && right == gempty
```

GroupTest.hs  
```haskell
import Group
import Test.QuickCheck

-- 群インスタンスの例
instance Group Int where
  gappend = (+)
  gempty  = 0
  ginv    = negate


-- 任意の元が法則を満たすことのテスト
grpTestAp :: IO ()
grpTestAp = let grpLawAp' = grpLawAp :: Int -> Int -> Int -> Bool
            in quickCheck grpLawAp'

grpTestEm :: IO ()
grpTestEm = let grpLawEm' = grpLawEm :: Int -> Bool
            in quickCheck grpLawEm'

grpTestInv :: IO ()
grpTestInv = let grpLawInv' = grpLawInv :: Int -> Bool
             in quickCheck grpLawInv'
```

長いですね。  
少しずつ見ていきましょう。
