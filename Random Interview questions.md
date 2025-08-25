## 1. Clientside rendering vs Serverside rendering
### Client-side rendering
Popular front-end frameworks will build and optimize code into HTML and Javascript bundles. When we access to a server, it will return a minimal HTML with the javascript bundles to our browser. Then our browser will perform to load the files into a complete web page.
#### Pros
- Much easier to handle user events, enable highly interactive experiences
- Faster subsequent navigations once the initial load is complete.
- Deployment infrastructure is more simple (1 FE app that can be run individually)
#### Cons
- Web page performance depends on client-side (internet, CPU). Performance is not consistent
- Business logic can be exposed in browser `Sources` tab
- Api calls is also public in `Network` tab
- Much more work and security measures needed in handling Authentication (localStorage, cookies)
- Web metrics score is low, SEO is not supported
### Server side rendering
Opposite to CSR, when we access to a server, the server will directly render HTML with the underlying business logic and return the complete web page to the browser. 
#### Pros
- Performance is consistent across clients
- Improve initial load speeds, making pages more accessible on slower networks.
- Business logic is hidden
- Handling authentication is more secure
- SEO-friendly because search engines can easily crawl fully-rendered pages.
#### Cons
- Some user events may break UX (rehydration)
- Don't have access to browser API (Geolocation , DOM api, Service workers, ...)
- Don't have information about client device/platform
- **Higher Time to First Byte (TTFB)**—generating pages dynamically on the server can introduce a delay.

Frameworks like **Next.js, Nuxt.js, and Angular Universal** offer built-in support for SSR and CSR, enabling developers to choose the best approach for each page.
## 2. Cookies vs SessionStorage vs Localstorage
### 2.1 SessionStorage
Is implemented from [Storage WebAPI](https://developer.mozilla.org/en-US/docs/Web/API/Storage) (You can add/update/remove stored item in the browser).
The data is stored in a page session, data is removed when page is closed.
#### Features
- A page session lasts as long as the tab or the browser is open, and survives over page reloads and restores.
	=> Closing tab/window ends page session and clear data in `sessionStorage`
- When a document is loaded, a unique page session gets created and assigned to that particular tab. 
	=> That page session is accessible only in that particular tab. The main document, and all embedded [browsing contexts](https://developer.mozilla.org/en-US/docs/Glossary/Browsing_context) (iframes), are grouped by their origin and each origin has access to its own separate storage area.
- If the page has a [`opener`](https://developer.mozilla.org/en-US/docs/Web/API/Window/opener "opener") (Opened by another page), the `sessionStorage` inherit a copy of the opener's `sessionStorage` object. However, they are still separate and changes to one do not affect the other. To prevent the `sessionStorage` from being copied, use one of the techniques that remove `opener` 
#### Usecase
- Autosave feature for textbox. Data is save even when page is refreshed.

### 2.2 LocalStorage
Also implements [Storage WebAPI](https://developer.mozilla.org/en-US/docs/Web/API/Storage)
Unlike `sessionStorage`, data stored in `localStorage` doesn't have expiry date and stays in multiple browsing session until deleted (Except for Private/Igconigto mode, data is cleared when all private tabs are closed).
#### Features
- Similar to session storage, data is separated into origins, page with different origin can't access other page's data. 
	**However**, `localStorage` data **is specific to the protocol of the document** (E.g `http://example.com` can't access data from `https://example.com`)
- The keys and the values stored with `localStorage` are in the [UTF-16](https://developer.mozilla.org/en-US/docs/Glossary/UTF-16) string format. As with objects, integer keys are automatically converted to strings.
- Can support large amount of data (5-10 MB)
- For documents loaded from `file:` URLs (files opened in the browser directly from the user's local filesystem) the requirements for `localStorage` behavior are undefined and may vary among different browsers.
#### Usecase
- Store user preferences/settings
- Access token (May need to prevent XSS carefully)

### 2.3 Cookies
A small, client-side dataset that contains information sent by the server. (~4 KB)
It is used to identify a client and acts as a way to maintain information about the client’s state in an otherwise stateless system.

#### Features
- Can use `Secure` attribute to enforce cookies only be transfer over `HTTPS`
- `HttpOnly` attribute to block access from Javascript
- `Expires` and `Max-Age`, cookies are expired given expiration date
#### Usecase
- **Tracking cookies** are used to build and maintain a browsing history for a client on a particular browser.
- **Authentication cookies** can be used to keep state-related information about a user that is currently logged in to the server. This type of cookie stores information about the user's account that can be used to continue a session. Without it, the user will have to [re-authenticate](https://http.dev/authentication "re-authenticate") each time a HTTP request is made.
- **Preferences** can be stored for the benefit of improving the user’s experience. For example, having a light or dark mode for a web page is user-specified customization that can persist between [HTTP sessions](https://http.dev/session "HTTP sessions").