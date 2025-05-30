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