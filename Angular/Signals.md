#tools 
Based on [SolidJs Signals]([Basics - Solid Docs](https://docs.solidjs.com/concepts/intro-to-reactivity#signals)) to apply reactivity programming. This programming paradigm refers to a system's ability to respond to changes in state automatically.

A `signal` is a wrapper function around a value, changes to value are tracked and notified to consumers automatically while maintaining synchronous programming. 

## **Writable signals**
To create a writable signals, call `signal` API with intial value. Without initial value it will be a readonly `signal`
```typescript
// Signals are getter functions - calling them reads their value.
const count = signal(0);
console.log('The count is: ' + count());
```

## **Computed signals**
Use `computed` API to create `signal` based on other `signal`. Created `signal` will be updated when other `signal` changes.

**Key features:**
- Lazy evaluation: Computation doesn't run intil dependencies change. See [[#Computed signals#**Example 3 ** `computed` signal dependencies are dynamic| Example 3]] 
- Memoization: Values from `computed` are cached and memoized until dependencies change.

**Note:** `computed` signals are readonly
### **Example 1:** `fullName` is updated when `firstName` changes
```typescript
const firstName = signal('Hieu');
const lastName = signal('Le');

const fullName = computed(() => `${firstName()} ${lastName()}`);
console.log(fullName()); // Hieu Le

firstName.update((name) => 'Ngoc Hieu');
console.log(fullName()); // Ngoc Hieu Le
```

### **Example 2:** `numberPower2` is updated when `number` changes
```typescript
const number: WritableSignal<number> = signal(0);
const numberPower2: Signal<number> = computed(() => number() ** 2;
```

### **Example 3:** `computed` signal dependencies are dynamic
```typescript
const showCount = signal(false);
const count = signal(0);
const conditionalCount = computed(() => { 
	if (showCount()) { 
		return `The count is ${count()}.`; 
	} else { 
		return 'Nothing to see here!'; 
	}
});
```

If `showCount` is false, `count` is not a dependency of `conditionalCount`. Unable to read `count` value.  
If `showCount` is true, `count` is a dependency of `conditionalCount`. Calling `conditionalCount()` again, we will see `count` value.

## **Effects**
>  An **effect** is an operation that runs whenever one or more signal values change

Effects always run **at least once.** When an effect runs, it tracks any signal value reads. Whenever any of these signal values change, the effect runs again.
Effects always execute **asynchronously**, during the change detection process.
Effects can only be executed in [Injection context](https://v19.angular.dev/guide/di/dependency-injection-context) such as:
- components, services, directives `constructor`
- Field initializer of classes
- Factory functions specified for `useFactory` of a `Provider` or an `@Injectable`.

```typescript
constructor() {
	effect(() => { 
		// console.log every time count changes
		console.log(`The current count is: ${count()}`);
	});
}
```

### **Use cases:**
Effects are rarely needed in most application code, but may be useful in specific circumstances. Here are some examples:
- Logging data (analytics or debugging).
- Sync data with `window.localStorage`.
- Adding custom DOM behavior that can't be expressed with template syntax.
- Performing custom rendering to a `<canvas>`, charting library, or other third party UI library.
**Note:** Avoid using `effects` to update state. This can leads to `ExpressionChangedAfterItHasBeenChecked` errors, infinite circular updates, or unnecessary change detection cycles.

### `untrack()` dependencies
Use `untrack` to read dependencies without tracking dependencies change.
The following example log a message each time for only `currentUser` changes and not `counter` changes.
If we don't use `untrack`, message is logged when `currentUser` or `counter` changes.
```typescript
effect(() => { 
	console.log(`User set to ${currentUser()} and the counter is ${untracked(counter)}`);
});
```

# [[RxJS]] Interoperability
The `@angular/rxjs-interop` package offers APIs that help you integrate RxJS and Angular signals.

## `toSignal`
Create a signal that tracks value of an `Observable`. 
Behaves similarly to `async` pipe in template. `toSignal` subscribes to `Observable` immediately.
The subscription created by `toSignal` automatically unsubscribes from the given Observable when the component or service which calls `toSignal` is destroyed.

```typescript
counterObservable = interval(1000); // Get a `Signal` representing the `counterObservable`'s value. 
counter = toSignal(this.counterObservable, { initialValue: 0 });
```

## `toObservable`
Create an `Observable` that tracks value of a `signal`.

```typescript
query: Signal<string> = inject(QueryService).query; 
query$ = toObservable(this.query); 
results$ = this.query$.pipe(
	switchMap(query => this.http.get('/search?q=' + query )) 
);
```