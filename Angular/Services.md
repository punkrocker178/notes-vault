# Declaring a service

```typescript
// hero.service.ts
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

> Is the part of the Angular framework that provides components with access to services and other resources. Angular provides the ability for you to _inject_ a service into a component to give that component access to the service

In order to inject a service to component, you have to provide it in the component level or the module level.
By default, Angular DI will look for the nearest scope which is in the current component `providers`, if this scope doesn't provide the service, Angular will continue to look upward which is the parent component. If component is already root component, Angular will look for `providers` in the Module. If Angular still doesn't find the service, it will throw `@NullInjector()` error

See the hierachical injectors in [[Angular DI]]