# Route config
```typescript
const routes: Routes = [
	{ path: 'first-component', component: FirstComponent },
	{ path: 'second-component', component: SecondComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Define an array of `Route` then add it to `RouterModule` and finally export it. 
We can now import `AppRoutingModule` in our desired module so the app can navigate to those components.

```typescript
@NgModule({
  declarations: [
    FirstComponent,
    SecondComponent
  ],
  imports: [
    CommonModule,
    BrowserModule,
    AppRoutingModule
  ],
  exports: []
})
export class AppModule
```

## Route order
Ordering route is very important as: 
> the `Router` uses a first-match wins strategy when matching routes, so more specific routes should be placed above less specific routes.

We should order specific routes at first, then  less specific routes (dashboards, list) and finally  [wildcard routes](https://angular.io/guide/router#setting-up-wildcard-routes) 

### Wild card routes
Wild card routes are routes that can match every URL.
A typical use case for this route is to navigate to Not found page when user go to a route that does not exist in our app.

```typescript
{ path: '**', component: PageNotFound },
```
# Other example
## Implement back button using Location
[Stackoverflow](https://stackoverflow.com/questions/74339620/how-can-i-navigate-back-the-url-in-angular-14)