# 最後に群！！

　最後に、群と呼ばれる構造です。

　群はモノイドに「逆元の存在」と呼ばれるものを足した構造です。[※1](#comment1)  
[Wikipedia](https://ja.wikipedia.org/wiki/%E7%BE%A4_%28%E6%95%B0%E5%AD%A6%29)

　半群、モノイドのページよりもなんだかコワイ感じですね。  
ですが恐れることはありません、ぴろぴろり〜ん。  
モノイドまで知っていれば以下の法則だけ注視していれば問題ありません。

> 逆元の存在  
> 群G のどんな元 g に対しても、 g • x = x • g = e となるような G の元 x が存在する

つまるところ`Int`と`(+)`の単位元`0`があって、適当な整数`5`に対して
```
5 + (-5) = (-5) + 5 = 0
```
という(-5)がありますよね、というだけなのです！

- - -

<a name="comment1">※1  </a>
余談ですが、モノイドも半群に「単位元律」を足した概念でしたね。  
つまるところ、モノイドは必ず半群であり、群は必ずモノイドでもあるのです
