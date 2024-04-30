那有什么方法能够防止这个漏洞吗？

37号issue最底下说到：

> libmcaptcha v0.2.2 implements queued validation with max queue length configuration.

其实就还是引入了一个IP limit...

不过mCaptcha这个思路真的挺好的，把IP limit + 手动拼图，弄成了 IP + “自动拼图”，加上ip queue之后，目前我觉得是没问题的。