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

```typescript
@Component({
  selector: 'app-component',
  templateUrl: './your-component.component.html',
  stylesUrl: ['./your-component.component.css']
})
```

## Directives

Compared to a `component`, `directive` is a class that can modify the behavior of an HTML element or a `component`.
`directive` apply directly to an element so we don't need to declare a template for it.  
`directive` also implements lifecycle methods same as a `component`
Most popular `directives` are:

- Structural directives: `*ngIf`, `*ngFor`
- Attribute directives: `ngClass`, `ngModel`

### Directive composition API (Angular 15) [Docs]([Angular - Directive composition API](https://angular.io/guide/directive-composition-api#directive-composition-api))

The API lets you apply directives to a component's host element from _within_ the component TypeScript class.

## Pipes

Pipes are special functions that are used in HTML templates to transform/modify display values.
Pipes can be chained together to output the desired value.
By using pipes, you have increased the reusability of the code base by declaring the transformation function once. So it can be used across many templates.

Usage:

```html
<span>{{ date | datePipe }}</span> <!-- Transform Date object into date string -->
<span>{{ totalValue | currency }} <!-- Transform number in to currency string -->
```

#### Built-in pipes
| Name                                                              | Description                                                                                   |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| [`AsyncPipe`](https://angular.dev/api/common/AsyncPipe)           | Read the value from a `Promise` or an RxJS `Observable`.                                      |
| [`CurrencyPipe`](https://angular.dev/api/common/CurrencyPipe)     | Transforms a number to a currency string, formatted according to locale rules.                |
| [`DatePipe`](https://angular.dev/api/common/DatePipe)             | Formats a `Date` value according to locale rules.                                             |
| [`DecimalPipe`](https://angular.dev/api/common/DecimalPipe)       | Transforms a number into a string with a decimal point, formatted according to locale rules.  |
| [`I18nPluralPipe`](https://angular.dev/api/common/I18nPluralPipe) | Maps a value to a string that pluralizes the value according to locale rules.                 |
| [`I18nSelectPipe`](https://angular.dev/api/common/I18nSelectPipe) | Maps a key to a custom selector that returns a desired value.                                 |
| [`JsonPipe`](https://angular.dev/api/common/JsonPipe)             | Transforms an object to a string representation via `JSON.stringify`, intended for debugging. |
| [`KeyValuePipe`](https://angular.dev/api/common/KeyValuePipe)     | Transforms Object or Map into an array of key value pairs.                                    |
| [`LowerCasePipe`](https://angular.dev/api/common/LowerCasePipe)   | Transforms text to all lower case.                                                            |
| [`PercentPipe`](https://angular.dev/api/common/PercentPipe)       | Transforms a number to a percentage string, formatted according to locale rules.              |
| [`SlicePipe`](https://angular.dev/api/common/SlicePipe)           | Creates a new Array or String containing a subset (slice) of the elements.                    |
| [`TitleCasePipe`](https://angular.dev/api/common/TitleCasePipe)   | Transforms text to title case.                                                                |
| [`UpperCasePipe`](https://angular.dev/api/common/UpperCasePipe)   | Transforms text to all upper case.                                                            |

#### Custom pipes

A pipe must have two things:

- A name, specified in the pipe decorator
- A method named `transform` that performs the value transformation.

```typescript
// kebab-case.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';
@Pipe({
  name: 'kebabCase',
})
export class KebabCasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toLowerCase().replace(/ /g, '-');
  }
}
```

## Services
## Resolvers
## Modules

## Guards
Functions to check whether route is allowed to navigate or not.
[[Guards]]
## Routing
Is a module to let user add routing config to application
[[Angular Routing]]