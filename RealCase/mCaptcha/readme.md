Unlike the ordinary Captchas, mCaptcha (mCaptcha/mCaptcha) uses SHA256 based proof-of-work (PoW) to rate limit users instead of the usual IP-based limit.

For a brief introduction, mCaptcha request the client to do some PoW work before sending the response.

It only takes little time to do such work in a normal machine, so it won't reduce the user experience so much.
Besides, by using mCaptcha, you'll never need to solve the annoying puzzles by your self.

However, for the bots, assumes it'll always take 0.1s to complete a mCaptcha, then if a hacker/bot trys to access your page for 1,000 times, it will take up 100s and will burn their machine first!
That's what attackers can't afford.

So, as the result, mCaptcha has once been considered as a more better way  to replace ordinary Captchas.

---

**---- (The contents below are copied directly from the mCaptcha project README) ----**

When a user wants to do something on a mCaptcha-protected website,

they will have to generate proof-of-work (a bunch of math that will takes time to compute) and submit it to mCaptcha.

We'll validate the proof:

if validation is unsuccessful, they will be prevented from accessing their target website
if validation is successful, read on,
They will be issued a token that they should submit along with their request/form submission to the target website.

The target website should validate the user-submitted token with mCaptcha before processing the user's request.

The whole process is automated from the user's POV. All they have to do is click on a button to initiate the process.

mCaptcha makes interacting with websites (computationally) expensive for the user. A well-behaving user will experience a slight delay (no delay when under moderate load to 2s when under attack; PoW difficulty is variable) but if someone wants to hammer your site, they will have to do more work to send requests than your server will have to do to respond to their request.