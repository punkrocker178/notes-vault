[[Angular Routing]]
Guards are functions that first run to check whether the conditions match when navigating to or exit a route.
1. ~~CanActivate~~ use CanActivateFn instead 
	If condition is `true`, allow to access this route
1. ~~CanDeactivate~~ use CanDeactivateFn instead
	If condition is `true`, allow to navigate to other route from current route
2. ~~CanLoad~~ use CanMatchFn instead
3. ~~CanMatch~~ use CanMatchFn instead
	If condition is `true`, navigation continues. If `false`, it will match other routes
# Class based `Route` guards deprecation
Angular 16 prefer functional guards, all `Route` guards interface are now deprecated.
Functional guards can be used directly in `Route` config

```typescript
const routes: Route[] = [
  {
    path: 'first-component',
    component: FirstComponent,
    canActivate: [() => inject(myGuard).canActivate()]
  }
];
```
