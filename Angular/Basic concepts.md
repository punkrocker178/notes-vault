## Component:

Components are the base building blocks of the application. It's a place where you can define logic and template altogether that can be reusable in the app. 
Each component consists of:
- HTML template
- Typescript class
- CSS styles

To define a component we need a `@Component()` decorator, the decorate allow us to create a component with lots of configurations, here are the most notable ones:
- `selector`: your component element name in HTML template
- `templateUrl`: path to HTML template, if you don't specify this option you can define template directly in `template` option
- `stylesUrl`: path to styles template, can be 1 or many
- `providers`: Provide component-level service for the dependency inversion
- `changeDetection`: Change detection strategy such as `default` or `onPush`
- `encapsulation`: Allow option to make your styling global or encapsulated to this component only
- `standalone`: An option to make a component standalone so it doesn't need to be declared in a module
- `imports`: If `standalone` is enabled, we need to use this option as well in order to add other components in the template

Example:
```
@Component({
  selector: 'app-component',
  templateUrl: './your-component.component.html',
  stylesUrl: ['./your-component.component.css']
})
```

## Directives
Compared to a `component`, `directive` is a smaller Typescript class that can modify the behavior of an HTML element or a `component`. `Directives` apply directly to an element so we don't need to declare a template for it.
Most popular `directives` are: 
- Structural directives: `*ngIf`, `*ngFor`
- Attribute directives: `ngClass`, `ngModel`
#### Directive composition API (Angular 15) [Docs]([Angular - Directive composition API](https://angular.io/guide/directive-composition-api#directive-composition-api))
The API lets you apply directives to a component's host element from _within_ the component TypeScript class.

## Pipes
## Services
## Resolvers
## Guards
## Module
## Routing