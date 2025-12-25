Used to be the most frustrating aspect in Angular. Due to the steep learning curve, Angular now recommends using standalone components from V18

# Angular Module Definition
Module is a subset of Angular components, services, directives, pipes, modules, ...etc combined altogether to become your application. 

>An NgModule has two main responsibilities:
> - Declaring components, directives, and pipes that belong to the NgModule
> - Add providers to the injector for components, directives, and pipes that import the NgModule

## Benefit of modularity
- Split up application features/business into smaller components, services, libraries to be more scalable, reusable.
- Modules then can be lazy loaded to reduce initial bundle size

## Example
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
	declarations: [AppComponent, MyComboboxComponent, CollapsibleDirective, CustomCurrencyPipe],
	imports: [BrowserModule],
	providers: [UserService, LessonsService]
})
export class ExampleModule {}
```

### `declarations`
Accepts _arrays_ of components, directives, and pipes. These arrays, in turn, may also contain other arrays.
### `imports`
Components, directives, pipes declared in this module may depend on other components, directives, pipes.   
So these dependencies needs to be added to the `imports` . Accepts _arrays_ of other `NgModule` or standalone components.
### `exports`
> An NgModule can _export_ its declared components, directives, and pipes such that they're available to other components and NgModules.  

NgModule can also exports components,directives, pipes of other `NgModule` that it imports.
### `providers`
Provide DI services to this module.
> These providers are available to:
> - Any standalone component, directive, or pipe that imports this module
> - The `declarations` and `providers` of any _other_ NgModule that imports this module.


## The `forRoot` and `forChild` pattern
> Some NgModules define a static `forRoot` method that accepts some configuration and returns an array of providers. The name "`forRoot`" is a convention that indicates that these providers are intended to be added exclusively to the _root_ of your application during bootstrap.

> Similarly, some NgModules may define a static `forChild` that indicates the providers are intended to be added to components within your application hierarchy.

In short, `forRoot` and `forChild`:
- `forRoot()` is for global setup (used when bootstrapping the app).
- `forChild()` is for localized setup (used deeper in the component tree).

### Use case of `forRoot`
Suppose we have a `AuthenticationService` and we want it to be instantiated once (Singleton). We have this service provided in `AppModule` (root module) and `SharedModule`. So that in our application and shared components can use `AuthenticationService`.  
But this will not work properly because we have create a new instance in `SharedModule` increasing the total instances of `AuthenticationService` to 2.  

To overcome this problem, we have to use `forRoot` pattern by declaring a static function.
```typescript
import {NgModule, ModuleWithProviders} from "@angular/core";
import {AuthenticationService} from "./authentication.service";

@NgModule({
	providers: [
		DataService,
		ThemeService,
		// AuthenticationService <-- If not removed, AuthenticationService is not singleton anymore
	]
})
export class SharedModule {
	static forRoot(): ModuleWithProviders {
		return {
			ngModule: SharedModule,
			providers: [AuthenticationService]
		};
	}
}
```
By removing the `AuthenticationService` from the `providers` in the `NgModule` metadata and return `ModuleWithProviders`, we have told Angular to provide the `AuthenticationService` of the root level to `SharedModule`

### Use case of `forChild`
Suppose we have a UI module and at a specific component down the copmonent tree, we want to have a different configuration compared to the root.
```typescript
@Component({
  providers: [CustomMenuModule.forChild({ color: 'blue' })]
})
export class UserProfileComponent {}
```
- This means: “Give the `UserProfileComponent` a version of `CustomMenuModule` with a blue theme.”
- The `forChild()` method returns configuration and providers tailored for just this spot in the app.

# References
1. [NgModules • Angular](https://angular.dev/guide/ngmodules/overview) (New docs have skipped alot of knowledge compared to v17.angular.io docs)
2. [Angular Modules and NgModule - Complete Guide](https://blog.angular-university.io/angular2-ngmodule/) (Summary of NgModule from legacy docs)