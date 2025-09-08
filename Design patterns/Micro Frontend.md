Think it as microservices for Frontend development.
Compared to Monolith, Micro frontend split big applications features into separate modules that are **independently** developed and deployed. 

**Monolith**
![Monolith FE](https://micro-frontends.org/ressources/diagrams/organisational/monolith-frontback-microservices.png)

**Micro Frontend**
![Micro FE](https://micro-frontends.org/ressources/diagrams/organisational/verticals-headline.png)

# Key benefits
- **Technology agnostic:** Each team can choose their tech stack, which leverage their expertise.
- **Independent development & deployment:** Each team has its own development lifecycle, which avoid dependencies from other teams. Enabling faster development and release cycles.
- **Fault isolation**: When a single microfrontend fails, it doesn't affect other modules or across application.
- **Improve Performance (Lazy loading):** Since code is splited into smaller parts, we only load necessary components in current page. Result in reduce initial app loading time.
- **Enhanced scalability:** The architecture scales well with both application growth and team expansion. New features can be added as independent micro frontends without impacting existing functionality.

# Implementation Approaches
## 1. single-spa library
## 2. Webpack 5 Module Federation
## 3. Web Component
## 4. Iframes