In theory, mCaptcha seems unbreakable.

However, there has been an issue talking about one way, that will attack the mCaptcha server itself. [See issue #37 in mCaptcha/mCaptcha.](https://github.com/mCaptcha/mCaptcha/issues/37#issuecomment-1206525955)

(English version hasn't completed.)

理论上来说，mCaptcha是无懈可击的。

但是，在[mCaptcha仓库的 #37 号issue](https://github.com/mCaptcha/mCaptcha/issues/37#issuecomment-1206525955)中，有个大蛇发现了一个方法，通过直接攻击 mCaptcha 服务器，使 mCaptcha 这个“防火墙”过载，从而更方便地进行DDoS或其他攻击。

让我们一起看看他的想法。

---
## 1
他的第一个漏洞直接命中了mCaptcha的要害——这个漏洞不是针对某个具体的代码，而是针对其原理。

你看，mCaptcha 会为所有的请求生成一个PoW任务对不对？然后等客户端返回答案后，再对答案进行验证。

所以mCaptcha服务器的算法一定包含——随机生成任务、验证任务两个部分。

这个大蛇提出的方法很有意思，说如果我攻击者的电脑不计算这个任务，直接返回一个随机数行不行？

比如说，服务器给我一道题`1+2=?`，我懒得算，直接返回一个`114514`。

这时候服务器收到了我的结果，他得验算对不对？他吭哧吭哧算了一下，`114514-2=114513≠1`，然后很得意地不返回html请求。

但是你看，我只是随机生成了一个随机数，他却要生成一个随机数 + 做一次验算，mCaptcha肯定要比我消耗更多资源，对不对？

那这时候，我只要开一万个虚拟机，疯狂生成随机数，这不就能扩大优势，把mCaptcha服务器弄瘫痪了吗？

> 原issue是这样写的：
> 
> start sending tons and tons of random PoW data to /api/v1/pow/verify ... for me that would take near to 0 CPU as I'm not actually computing the PoW, but what for the verification process in the server?

所以，关键就在于赢得那一点点小的优势，通过bot的数量能快速翻倍，成为显著的优势。

这是一个黑客技巧。



## 2
第二个漏洞是基于第一个漏洞的，属于增强版。

第二个漏洞是这样的：

如果你重复请求了n次，那么你很可能就是bot，按照mCaptcha的代码实现，就会给你升一个难度。

这样一来，再用上第一个漏洞，我在开头先手动刷100次请求，把难度升到最高。

题目的难度搞了，老师验算的难度也就高了，所以这时候再发动第一部分所述的攻击，就能更快搞死mCaptcha。

所以作者原文那段话其实是这样的：

> I can perform 50 requests to /api/v1/pow/config (just to increase the difficulty factor, without computing the PoW) and then start sending tons and tons of random PoW data to /api/v1/pow/verify ... for me that would take near to 0 CPU as I'm not actually computing the PoW, but what for the verification process in the server?


