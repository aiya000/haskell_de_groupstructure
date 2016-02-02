## 逆元の存在

　逆元とは、「それ」と演算をすると結果が単位元になるものです。

```haskell
instance Group Int where
  gappend = (+)
  gempty  = 0
  ginv    = negate
```

上の「`Int`と`(+)`の群」の場合は…適当な数`7`を取り上げると  
```
7 + (nagate 7) = (nagate 7) + 7 = 0
```
を満たしますね。  
これは以下と同じです。  
```
7 + (ginv 7) = (ginv 7) + 7 = 0
```

- - -

　この法則(逆元の存在)を表すコードが以下です。  
`grpLawInv`が法則を表し、`grpTestInv`でそのテストを行っています。

```haskell
grpLawInv :: (Group a, Eq a) => a -> Bool
grpLawInv x =
  let left  = x `gappend` (ginv x)
      right = (ginv x) `gappend` x
  in left == right && right == gempty

grpTestInv :: IO ()
grpTestInv = let grpLawInv' = grpLawInv :: Int -> Bool
             in quickCheck grpLawInv'
```
