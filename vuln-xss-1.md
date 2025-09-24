\# vuln-xss-1.md



\## Title

Reflected XSS in Juice Shop search parameter



\## Date

YYYY-MM-DD



\## Target

OWASP Juice Shop (local Docker)



\## Summary

A reflected cross-site scripting (XSS) vulnerability was found in the search endpoint which allows injection of arbitrary HTML/JS into the response.



\## Affected endpoint / URL

e.g. http://localhost:3000/#/search?q=...



\## Proof of Concept (PoC) - steps to reproduce

1\. Start Juice Shop: `docker run --rm -p 3000:3000 bkimminich/juice-shop`

2\. Configure browser to use proxy at `127.0.0.1:8080` and open Burp.

3\. Go to the search box and intercept the search request with Burp Repeater.

4\. Replace the search parameter value with: <iframe src="javascript:alert('XSS')">

5\. Send the request and observe the response reflects the payload.



\## Screenshots

screenshots/xss-request.png

screenshots/xss-alert.png



\## Severity

Medium / High



\## Impact

An attacker could trick a user into visiting a crafted URL and execute JavaScript in the context of the site, possibly stealing cookies or performing actions as the user.



\## Remediation

1\. Contextual output encoding.

2\. Use templating engines that escape output.

3\. Add CSP as defense-in-depth.



\## Verification

Repeat the PoC and confirm payload is escaped or CSP blocks inline scripts.





