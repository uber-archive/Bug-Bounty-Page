Program Update April 28 2016 
==
Payouts Clarification

There has been some confusion around the way we do rewarding in our bug bounty program. Our rewards are solely impact based, meaning that we look at what can be done with a bug and reward based on the impact to both the business and our customers.

To clarify, we want to explain some of the logic behind “impact.” For example, we rank vulnerabilities in our production data center much higher than vulnerabilities in third-party services because a real-world attacker could do much more damage in our production data center than with control over one of our WordPress blogs hosted on WP Engine. The former could compromise customer information, while the latter essentially allows defacement of an Uber branded website—no personal information is stored there.

When we have our reward meetings, we always ask one question: If a malicious attacker abuses this, how bad off are we? We assume the worst and pay out the bug accordingly.

We’d also like to clarify how we handle payout in the case of multiple vulnerability reports in a single component of our systems. For our WordPress blogs, for example, we often get reports that list many vulnerabilities in a single plugin. These submissions are unique because, despite the component having multiple vulnerabilities, the fix is the same: remove the vulnerable plugin. In these situations, we opt to reward a bounty for the highest risk issue submitted instead of paying each issue out individually. The reasoning for this is due to the possibility of receiving a submission on a WordPress plugin with 30 separate cross-site scripting (XSS) vulnerabilities. It doesn’t make sense to pay out tens of thousands of dollars when the remediation is just removing the poorly designed plugin. For fairness, we bump up payouts for these submissions if the researchers put extra effort into finding these issues. We handle this determination case by case.

At the end of the day, rewarding is done at our discretion. Some researchers won't agree with some of our decisions, but we're paying out to the best of our ethical ability and trust that the majority of researchers will consider their rewards fair and even generous. We will adapt as the program continues.


Program update April 14 2016
==

* Removed "rate limiting" from Medium issues description. It is always at our discretion how much to reward an issue and we do so based on the impact to ubers customers, data, code and employees. Our motivation is to reward as much as possible for great issues. That said the payout ranges below are intended as rough guidance on how we categorize issues, not a strict rubric.

Program update April 11 2016
==
Thank you everyone for the outpouring of attention, effort, and bugs. 

Our public bug bounty has been live for a few weeks now and we have been impressed with the great reports we have seen. We are adjusting our scope based on what we have learned to best encourage research on the areas most likely to be rewarded


No longer in scope as of 4/11/2016
====
* *.dev.uber.com
* Open redirects - 99% of open redirect issues have low security impact. For the rare cases, like stealing oauth tokens, we do still want to hear about them
* *.et.uber.com - The underlying software here is exacttarget which Uber does not have control over. They have requested to be removed. 
* Publicly accessible login panels - These generally have low security impact and are in software that Uber runs but doesn’t control. 
* Reports that state that software is out of date/vulnerable without a proof of concept.
* XSS issues in non-current browsers. 
* Stack traces disclosing information
* “CSV injection” - see: https://sites.google.com/site/bughunteruniversity/nonvuln/csv-excel-formula-injection
* Uber-finder.com - this is not software owned by Uber engineering. 

Now in scope as of 4/11/2016
===
* *.uberinternal.com - anything here is internal software used by Uber the company. We may not be able to fix flaws found here as quickly as we are beholden to other companies
* Bulk vehicle uuid enumeration - any instance where you could collect a lot of vehicle uuids is interesting to us based on the circumstances. 

To get a list of your vehicle UUIDs, navigate to https://partners.uber.com/vehicles/ and paste the following into your browser’s development console:
```js
vuids = document.querySelectorAll( "#vehicle-uuid" );for( var i = 0;i<vuids.length;i++){console.log( vuids[i].value )};
```
Generally speaking, any request which allows you to enumerate bulk vehicle UUIDs for accounts is considered an issue we are concerned about.

These changes go into effect today but any issues submitted before then will be evaluated against the old program scope. 

How are payouts done for dupes?
===
If we receive several reports for the same issue, we offer the bounty to the earliest report for which we had enough actionable information to identify the issue. We dont want to encourage people spamming us with vague issues in an attempt to be first. 



Want to blog about your bug?
===
We have received questions about blog posts about bugs. To be clear, we love it! We just ask that you wait until the issue is both fixed and paid out before you publish the blog. We also prefer that you request disclosure through hacker1 for an issue as full background for anyone reading your blog post. Any questions around this just let us know and we would be happy to help out.

Payouts
====
It is important to mention the payout ranges on this page are guidelines to express roughly how we think about the severity of families of issues. They are not exact rules. There can be attributes of bugs that make them more or less severe, which will affect the payout. So far we have most commonly rewarded on the top end of the ranges. 

Accepted report requirements
====
We no longer accept reports with only a video, but need detailed written repro steps

Program terms
===
Your participation in the Bug Bounty Program is voluntary and subject to the [Bug Bounty Program Terms](https://www.uber.com/legal/other/bug-bounty-program-terms/).


What type of vulnerabilities is Uber looking for?
===
At Uber we are looking for any vulnerability which could negatively affect the security of our users. The main categories of vulnerabilities that we look for are the following:

* Cross-site Scripting (XSS)
* Cross-site Request Forgery
* Server-Side Request Forgery (SSRF)
* SQL Injection
* Server-side Remote Code Execution (RCE)
* XML External Entity Attacks (XXE)
* Access Control Issues (Insecure Direct Object Reference issues, etc)
* Exposed Administrative Panels that don't require login credentials
* Directory Traversal Issues
* Local File Disclosure (LFD)


Please note that if a vulnerability (such as XSS) only affects a small population, e.g. a browser with a low usage percentage, the reward will be determined accordingly. Vulnerabilities that exist only in antiquated browsers such as Internet Explorer 8 for example, are not in scope.

What type of vulnerabilities is Uber NOT looking for?
===
The following are  vulnerabilities which Uber does not consider severe enough for a reward:

* Best practices concerns. 
* Highly speculative reports about theoretical damage. Be concrete. 
* Self-XSS that can not be used to exploit other users (this includes having a user paste JavaScript into the browser console)
* Vulnerabilities as reported by automated tools without additional analysis as to how they're an issue
* Denial of Service Attacks
* Reflected File Download (RFD)
* `window.opener` Related Issues
* Physical or social engineering attempts (this includes phishing attacks against Uber employees)
* Content injection issues
* Non-validated reports from automated web vulnerability scanners (Acunetix, Vega, etc)
* Cross-site Request Forgery (CSRF) with minimal security implications (Logout CSRF, etc.)
* Missing autocomplete attributes
* Missing cookie flags on non-security sensitive cookies
* Issues which require physical access to a victim’s computer
* Missing security headers which do not present an immediate security vulnerability
* Fraud issues (please see the below section elaborating on this)
* SSL/TLS scan reports (this means output from sites such as SSL Labs)
* Banner grabbing issues (figuring out what web server we use, etc)
* Open ports without an accompanying proof-of-concept demonstrating vulnerability
* Open Redirect Vulnerabilities
* Publicly accessible login panels
* Recently disclosed 0day vulnerabilities. We need time to patch our systems just like everyone else - please give us two weeks before reporting these types of issues.


Things you should expect to recieve low to no bounty for
==
* Microsites with little to no user data
* Issues requiring user-interaction
* Outdated wordpress instances
* Most brute forcing issues


What is your policy on chaining bugs and privilege escalation?
===
Chaining of bugs is not frowned upon in any way, we love to see clever exploit chains! However, if you have managed to compromise an Uber-owned server we do not allow for escalations such as port scanning internal networks, privilege escalation attempts, attempting to pivot to other systems, etc. If you get access to an Uber server please report it us and we will reward you with an appropriate bounty taking into full consideration the severity of what could be done. Chaining a CSRF vulnerability with a self XSS? Nice! Using AWS access key to dump user info? Not cool.

Do you provide test accounts?
===
As of this time we do not have a good system for creating test accounts for our bug bounty submitters. Please create an account as you would normally and perform testing with that account or accounts.  Whenever possible only test against yourself, never other users. If there is ever a situation where you cannot test a bug while adhering to this please let us know and we will help figure out an appropriate solution. 

What is a user UUID and when do you reward for enumeration of it?
===
We reward for issues which allow you to enumerate bulk user UUID's via a phone number or email address. For example, if there's an endpoint that allows you to submit an email and the response contains that user's UUID - this is a vulnerability we would reward for. To verify this you should compare the UUID you're seeing with your own email. To get your personal account UUID visit `help.uber.com` after authenticating and copy and paste the following JavaScript in your browser's developer console:
```js
alert(JSON.parse($("#web-support-data-script").text).user.uuid);
```
(We reward for this bug because we want to make it harder to perform bulk insecure direct object reference attacks against our users).

What is in scope for this program?
===
* https://*.uber.com/
* http://petition.uber.org
* http://ubermovement.com
* iPhone Rider Application
* iPhone Partner Application
* Android Rider Application
* Android Partner Application

What about public disclosure?
===
Found a particularly interesting or clever bug in an Uber service? We’re more than happy to publicly disclose your bug once it has been remediated by our developers. Please note that in certain situations we may request more time to investigate an issue internally to ensure that it is properly fixed across all Uber services. Public disclosure before Uber has had time to remediate an issue is grounds for immediate forfeiture of any reward as well as possible removal from the bug bounty program.

What is an Uber microsite?
===
An Uber microsite is a website which is not explicitly listed in the scope above but is made by an Uber employee and owned by Uber. The most common examples of microsites include Uber city sites, blogs, and partner incentive sites.

Are Uber microsites (for example, our blogs and city-specific Uber sites) in scope?
===
Microsites are an important part of how Uber reaches people in diverse local markets all around the world. Since they have smaller audiences, shouldn't contain much or any user data and aren’t part of the our core services, the impact of issues on these sites is significantly less severe. Since we are primary interested in vulnerabilities which could lead to the exfiltration of customer information, vulnerabilities in microsite services will not be rewarded for except in extraordinary circumstances. Generally there are [better areas](https://eng.uber.com/bug-bounty/) to spend your time than microsites.



Fraud related issues. 
===
If you’d like to report an issue with our fraud, please contact ext-uber-fraud@uber.com. These type of issues are important but we unfortunately cannot reward issues if this type at this time. Specifically promo code fraud and give-get fraud is abuse of our promotional offers and referral codes in order to get free rides from Uber are a common submission. We do not consider these in scope for our bug bounty program at this time unless they show an explicit technical vulnerability in our software.  Lack of verification for things such as phone numbers, credit cards, etc are all fraud related issues and are not in scope for this bug bounty program.

Bounty Payout Range
===
N.B: the amounts listed here are the maximum we can pay for these categories of issues. This is meant as rough guidance on how we think about rewarding issues, ultimately we will reward largely based on the impact of the issue but at our discretion. 

* **Critical issues ($10,000)** - Remote code execution on a production server. Exposure of information that identifies individuals (social security numbers, credit card numbers, bank account numbers, driver license images) Full account takeover of rider/partner account without interaction. Payment or partner invoice information exposure at scale. Potential access to source code. XSS in Toolshed (our internal account management system), or server-side request forgery (SSRF). Vulnerabilities leading to the compromise of an employee account (with a way to bypass two-factor).

* **Significant Issues ($5,000)** - Stored Cross-site Scripting which can cause significant brand damage (e.g. in a homepage), missing authorization checks leading to the exposure of email addresses, date of birth, names, phone numbers, etc.

* **Medium Issues ($3,000)** - Reflected Cross-site Scripting (XSS), most Cross-site Request Forgery (CSRF) issues, access control issues which do not exposed PII but affect other accounts, some account validation bypasses (being able to change driver picture, etc). Any vulnerability which allows the bulk lookup of user UUIDs (e.g. turn an auto-incrementing ID into a UUID, turn an email into a UUID).

* **Fraud Issues** - Send these to `ext-uber-fraud@uber.com`. We currently do not reward for fraud issues. 

Examples of good bugs
==

* https://fin1te.net/articles/uber-turning-self-xss-into-good-xss/
* http://blog.portswigger.net/2016/04/adapting-angularjs-payloads-to-exploit.html
* http://blog.orange.tw/2016/04/bug-bounty-uber-ubercom-remote-code_7.html

-----
*Psst, this is a [Github repo! Wondering if there was a recent rule change? Click here!](https://github.com/uber/Bug-Bounty-Page)*
