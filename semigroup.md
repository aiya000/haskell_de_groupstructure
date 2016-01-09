## 本記事で紹介するイカれたメンバーを紹介するぜ！

### まずは半群！！

半群は以下のような構造です。
[Wikipedia](https://ja.wikipedia.org/wiki/%E5%8D%8A%E7%BE%A4)

モノイドを知っている人はわかったかもしれませんが、半群はモノイドから「単位元」を抜き去った構造です。  


```haskell
import Test.QuickCheck

class Semigroup a where
  sappend :: a -> a -> a

sgLaw :: (Semigroup a, Eq a) => a -> a -> a -> Bool
sgLaw x y z = (x `sappend` y) `sappend` z == x `sappend` (y `sappend` z)

instance Semigroup Int where
  sappend = (*)

sgTest1 :: IO ()
sgTest1 = let sgLaw' = sgLaw :: Int -> Int -> Int -> Bool  -- QuickCheckのために単相化
          in quickCheck sgLaw'
```

- - -

　上の半群は「整数と乗算の半群」と呼ばれるものです。  
Wikipediaの言葉と合わせて見ていきましょう。

> 集合 S とその上の二項演算 • : S × S → S が与えられたとき、組 (S, • ) が以下の条件を満たすならば、これを半群という。

　今回の集合Sは、「Int」です。  
つまり64bit CPUであれば`-2147483648 〜 2147483647`という数全ての集合です。

また、sappend関数で指定している通り、二項演算・とは(\*)演算子のことです。

> 二項演算 • : S × S → S

とはHaskellで書くと
```haskell
(*) :: Int -> Int -> Int
```
ってことです。

この時のInt, (\*)を合わせてそれらが__以下の条件__を満たすならば「半群」と言います…ということですね。

- - -

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
