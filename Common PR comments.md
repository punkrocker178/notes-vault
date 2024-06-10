- Reduce using if statements in observer by using `filter` pipe
```typescript
/* Avoid using */
confirmationDialog.afterClosed().subscribe(confirmed => {
  if (confirmed) {
    // do something
  }
});

/* Suggestion */
confirmationDialog.afterClosed()
.pipe(filter(confirmed => !!confirmed))
.subscribe(confirmed => {
  // do something
});
```

- Injected services should have `readonly` attribute
```typescript
constructor(
  private readonly _notification: NotificationService,
) {
}
```

- Should add `public` access modifiers to property of a class (model)
```typescript
export class Entity {
  public id: number;
  public name: string;
}
```
