App intialization is configured in `main.ts`
Since standalone component is a thing now, so there are 2 ways to intialize an Angular application
#### Bootstrap module

My prefered method, using this method, we have to declare `AppModule` with some basic imports and declare which component to be bootstraped
```typescript
// AppModule
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    CommonModule,
    BrowserModule,
    AppRoutingModule,
    HttpClientModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }

// main.ts
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```
#### Bootstrap standalone component
This method skip the Application module declaration, therefore reducing boiler plate code.

The root component to be bootstraped must be `standalone: true`
```typescript
// main.ts
export const appConfig: ApplicationConfig = {
	providers: [
		provideZoneChangeDetection({ eventCoalescing: true }),
		provideRouter(routes)
	]
};

bootstrapApplication(AppComponent, appConfig)
	.catch((err) => console.error(err));
```

The differences between the 2 methods are the former uses
`platformBrowserDynamic().bootstrapModule` while the latter uses `bootstrapApplication`