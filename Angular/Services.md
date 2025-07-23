# Declaring a service as dependency

```typescript
// hero.service.ts
@Inject()
export class HeroService {
  private heroes: Hero[] = [];

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`);
      this.heroes.push(...heroes); // fill cache
    });
    return this.heroes;
  }
}
```

Use in component by dependency injection

```typescript
@Component({
	selector: 'app-dashboard',
	standalone: true,
	templateUrl: './dashboard.component.html',
	styleUrl: 'dashboard.component.scss',
	providers: [HeroService]
})
export class DashboardComponent {
	constructor(
		private _heroService: HeroService
	)

	// Implementation
}
```

# Dependency Injection (DI)

### Injectable() Decorrator
>Decorator that marks a class as available to be provided and injected as a dependency.

```
@Injectable({ 
  providedIn?: Type<any> | "root" | "platform" | "any" | null | undefined;
})
```
`providedIn` values are:
- 'root': The application-level injector. A singleton instance that is available in the entire application
- 'platform':  _A special singleton platform injector shared by all applications on the page_. Which is useful when sharing a single service instance across [Angular Elements]([Custom Elements • Angular](https://angular.dev/guide/elements))

> Is the part of the Angular framework that provides components with access to services and other resources. Angular provides the ability for you to _inject_ a service into a component to give that component access to the service

In order to inject a service to component, you have to provide it in the component level or the module level.
If  the dependency is not provided as root level, Angular DI will look for the nearest scope which is in the current component `providers`, if this scope doesn't provide the service, Angular will continue to look upward the hierachical tree, which is the parent component. If component is already root component, Angular will look for `providers` in the NgModule. If Angular still doesn't find the service, it will throw `@NullInjector()` error

See the hierachical injectors in [[Angular DI]]