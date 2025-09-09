#tools
### Observables
> An Observable is a Producer of multiple values, "pushing" them to Observers (Consumers).

```typescript
const observable = new Observable(function subscribe(observer) { 
	// const id = setInterval(() => observer.next('hi'), 1000); 
	[1,2,3].forEach(num => {
		observer.next(num);
	});
	subscriber.complete();
});

const observer = {
	next: (value) => {
		console.log(value);
	}
};

observable.subscribe(observer);
//Logs:
// 1
// 2
// 3
```

The above example is equivalent to
```typescript
const observable = from([1,2,3]);
const observer = {
	next: (value) => {
		console.log(value);
	}
};

observable.subscribe(observer);
```
### Subjects
> An RxJS Subject is a special type of Observable that allows values to be multicasted to many Observers.
> While plain Observables are unicast (each subscribed Observer owns an independent execution of the Observable), Subjects are multicast.

There are 4 types of Subjects:
- `Subject`: Plain `Subject` doesn't have intial value. Since `Subject` are an Observer, we can provide a `Subject` as an argument for any `Observerble` to make an `Observable` multicast.
- `BehaviorSubject`: Similar to `Subject`, but have initial value. We can get the latest value even after new value has already emitted.
- `ReplaySubject`: Can replay old values to new subscriber, can specify how many records to replay. 
- `AsyncSubject`: Similar to `last()` operator, it waits for `complete()` notification inorder to deliver a value.

#### `Subject` as Observer
```typescript
const subject = new Subject<number>();
subject.subscribe({
	next: (v) => console.log(`observerA: ${v}`),
});
subject.subscribe({
	next: (v) => console.log(`observerB: ${v}`),
});

const observable = from([1, 2, 3]);
observable.subscribe(subject); // You can subscribe providing a Subject

// Logs:
// observerA: 1
// observerB: 1
// observerA: 2
// observerB: 2
// observerA: 3
// observerB: 3
```
### Operators
#### Transformation
- `concatMap`
- `switchMap`
- `mergeMap`

#### Combination
- `combineLatest`
- `pairwise`
- `withLatestFrom`
- `startWith`

#### Creation
- `of`
- `timer`
- `from`
- `fromEvent`

#### Filter
- `take`
- `takeUntil`
- `filter`
- `firts`
- `debounceTime`
- `auditTime`
- `skip`

#### Utility
- `tap`
- `delay`
- `finalize`
