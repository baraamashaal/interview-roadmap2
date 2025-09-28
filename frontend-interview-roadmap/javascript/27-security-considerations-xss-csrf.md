# 27. Security Considerations (XSS, CSRF) in JavaScript

## Quick Revision

Two of the most common web security vulnerabilities are Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF).

*   **Cross-Site Scripting (XSS):** An attack where a malicious script is injected into a trusted website. The script then runs in the user's browser and can be used to steal cookies, session tokens, or other sensitive information.

*   **Cross-Site Request Forgery (CSRF):** An attack that tricks a user into performing an unwanted action on a website they are authenticated on. The attacker forges a request and sends it to the user, who then unknowingly executes it.

## Detailed Explanation

### Cross-Site Scripting (XSS)

XSS attacks occur when an application includes user-provided data in its output without properly sanitizing it.

#### Types of XSS

1.  **Stored XSS:** The malicious script is permanently stored on the target server (e.g., in a database). When a user visits a page that includes the stored script, it is executed.
2.  **Reflected XSS:** The malicious script is reflected off a web server, such as in a URL or an error message. The script is not stored on the server.
3.  **DOM-based XSS:** The vulnerability exists in the client-side code. The attacker manipulates the DOM to execute the malicious script.

#### How to Prevent XSS

*   **Sanitize user input:** Never trust user input. Always sanitize it before rendering it on the page. Use libraries like `DOMPurify`.
*   **Use `textContent` instead of `innerHTML`:** When inserting text into the DOM, prefer `textContent` as it does not parse the HTML.
*   **Content Security Policy (CSP):** Use a CSP to specify which sources of content are allowed to be loaded on your site.

### Cross-Site Request Forgery (CSRF)

CSRF attacks exploit the trust that a site has in a user's browser. If a user is logged into a site, their browser will automatically include their session cookie with any request to that site.

An attacker can create a malicious website that sends a request to the target site. If the user visits the malicious site while logged into the target site, the request will be sent with their session cookie, and the target site will treat it as a legitimate request.

#### How to Prevent CSRF

*   **Anti-CSRF Tokens:** The most common defense against CSRF. The server generates a unique, random token for each user session and includes it in a hidden form field. When the user submits the form, the server checks if the token matches.
*   **SameSite Cookies:** The `SameSite` cookie attribute can be used to control whether cookies are sent with cross-site requests.
    *   `Strict`: The cookie is only sent with requests from the same site.
    *   `Lax`: The cookie is sent with same-site requests and with top-level navigations.
    *   `None`: The cookie is sent with all requests.
*   **Check the `Origin` or `Referer` header:** You can check the `Origin` or `Referer` header of a request to see where it came from.

## Code Examples

### XSS Prevention (using `textContent`)

```javascript
const userInput = '<img src="invalid-image" onerror="alert(\'XSS attack!\')">';

// Insecure: uses innerHTML
// document.getElementById('output').innerHTML = userInput;

// Secure: uses textContent
document.getElementById('output').textContent = userInput;
```

### Anti-CSRF Token Example (Conceptual)

```html
<form action="/update-profile" method="POST">
  <input type="hidden" name="_csrf" value="your-random-token">
  <input type="text" name="email">
  <button type="submit">Update</button>
</form>
```

On the server side (e.g., with Node.js and Express):

```javascript
app.post('/update-profile', (req, res) => {
  if (req.body._csrf !== req.session.csrfToken) {
    return res.status(403).send('Invalid CSRF token');
  }
  // ... update profile
});
```

## Resources

*   **Article:** [OWASP - Cross-Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/)
*   **Article:** [OWASP - Cross-Site Request Forgery (CSRF)](https://owasp.org/www-community/attacks/csrf)
*   **Video:** [Cross-Site Scripting (XSS) - Computerphile](https://www.youtube.com/watch?v=L5l9lSnNMxg)
*   **Video:** [Cross-Site Request Forgery (CSRF) - Computerphile](https://www.youtube.com/watch?v=eWEg_YLgwoA)
