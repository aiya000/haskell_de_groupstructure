## Monoidインスタンスがモノイドである条件について

　今回注視すべきは「単位元律 = `mnLawEm`」です。

```haskell
-- 単位元律
mnLawEm :: (Monoid a, Eq a) => a -> Bool
mnLawEm x =
  let left  = mempty `mappend` x
      right = x `mappend` mempty
  in left == right && right == x
```

少々コード化すると見難くなっていますが、Wikipediaから引用すると以下のことを表しています。

> 単位元律
>     S の元 e が存在して、S の任意の元 a に対して e • a = a • e = a

　実はこのWikipedia中の`e`は、`mempty`と同一です。

`mnLawEm`は、例えば`a = 3`に対して以下になることを表しています。
(「`mappend` = •」は`(*)`です)

```
1 * 3 = 3 * 1 = 3
```

`mnTestEm1`は`Monoid Int`が`mnLawEm`を満たしていることをテストしています。
