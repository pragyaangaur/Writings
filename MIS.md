# 12 A.M. on my College MIS

25/05/2026

---

I only logged into the college MIS (Management Information System) to check my attendance, but the structural integrity of this system is so completely broken I couldn't look away.

To understand the flaw, you just have to look at the network tab. They attempted client-side AES-128 encryption on the login, which sounds reassuring until you see they hardcoded the key (`redacted`) right into the public JavaScript.

Then there’s the CAPTCHA. Mechanically, this should act as a barrier of high density to filter bots. Instead, the CAPTCHA value is sitting in plain text (e.g., `d80c44`) inside an HTML tag. You could write a script to scrape it in two seconds. Combined with zero rate limiting on the login, this structure collapses instantly under automated pressure.

But you wouldn't even need to credential-stuff. The "Forgot Password" flow is a total backdoor. It generates a 5-character alphanumeric OTP with absolutely no attempt limits. The combinatorial space is merely:

$$S = 36^5 \approx 60.4 \text{ million possibilities}$$

That is a mathematical space you can brute-force before their generous 120-second timer even runs out. 

And once you're in? The authenticated URL appends an `?enc=` parameter. You can delete the value and send the request anyway. The session stays completely open.

It's actually terrifying how exposed this is. The next time you check your grades, you are briefly turning your academic records into an open boundary condition for the public internet. 

> *Disclaimer: All observations described here were made through examination of publicly delivered client-side code and behavior associated with my own account. No unauthorized access, privilege escalation, or access to other users’ data was performed. A responsible disclosure report will be provided to the relevant administrators.*
