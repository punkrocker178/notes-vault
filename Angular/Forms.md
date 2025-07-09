Reference from [Forms Overview]([Forms • Overview • Angular](https://angular.dev/guide/forms))
[Stack blitz](https://stackblitz.com/edit/stackblitz-starters-izevjza2?file=src%2Fcomponents%2Fform-tester%2Fform-tester.html)
# Template-driven forms

Use directives `ngForm`, `ngModel` to implicit create form controls on template. This approach is a quick and simple way to implement forms, the model that binds to a form control is directly updated by `ngModel`.

>Rely on directives in the template to create and manipulate the underlying object model. They are useful for adding a simple form to an app, such as an email list signup form. They're straightforward to add to an app, but they don't scale as well as reactive forms. If you have very basic form requirements and logic that can be managed solely in the template, template-driven forms could be a good fit.|

## Usage
In component file
```typescript
public personName: string;
public personAge: string;

public submit() {
	console.log(this.personName, this.personAge);
}
```

In template file
```html
<form (ngSubmit)="submit()">
	<label for="name">Name </label>
	<input id="name" name="name" type="text" [(ngModel)]="personName"/>

	<label for="age">Age </label>
	<input id="age" name="age" type="text" [(ngModel)]="personAge"/>
	<button type="submit">Submit</button>
</form
```

From a very simple setup above, we now have a fully functional form that can store user input.  
The directive `ngModel` is wrapped as `[()]` banana in a box, which is two-way binding. 
Two-way binding means the model can input data into the directive `ngModel` and `ngModel` can output data into model. 
## Data flow
This section will explain more about `ngModel` two-way binding works.
### View to model
1. User input value to the `<input>` element
2. `<input>` element emit value change event to the ControlValueAccessor
3. The ControlValueAccessor triggers the `setValue()` method on the `FormControl` instance.
4. The `FormControl` instance emits the new value through the `valueChanges` observable.
5. The ControlValueAccessor also calls the `NgModel.viewToModelUpdate()` method which emits an `ngModelChange` event.
6. `ngModelChange` event is an output emitted to the model, in this case it is `personName`. 
7. In this scenario, we are using the output binding `(ngModel)=personName`
### Model to view
1. Component model `personName` is updated programatically
2. Change detection begins.
3. During change detection, the `ngOnChanges` lifecycle hook is called on the `NgModel` directive instance because the value of one of its inputs has changed.
4. The `ngOnChanges()` method queues an async task to set the value for the internal `FormControl` instance.
5. Change detection completes.
6. On the next tick, the task to set the `FormControl` instance value is executed.
7. The `FormControl` instance emits the latest value through the `valueChanges` observable.
8. TheControlValueAccessor updates the form input element in the view with the latest value.
9. In this scenario, we are using input binding `[ngModel]=personName`

### Listen for value changes
It is not stated in the docs, means this approach should not be handled in a reactive way.
However, we still can do the traditional `change` event
```html
<label for="name">Name </label>
<input id="name" name="name" type="text" [(ngModel)]="personName" (change)="handleNameChange($event)"/>
```

DOM `change` event can emit values whenever user input changes, we can access this value by passing `$event` into the method. As stated above, this kind of implementation is not recommended as this affect performance by triggering multiple changeDetections. Additionally, we don't have much control over the flow of events. Meaning, we have to implement a custom `debounce` and `throttle` function to mitigate the number of events fired to avoid performance loss.

Another method is to `@ViewChild` the `<form>` element. This way, we can access to the `ngForm` directive and it's `FormGroup`. 
A `FormGroup` containing multiple `FormControl`s that are bound with `ngModel`. We can listen to value changes of these form controls. But doing this, we are basically using ReactiveForms !
```typescript
@ViewChild('form') ngForm!: NgForm;
ngOnInit(): void {
    setTimeout(() => {
      this.ngForm.form.controls['name'].valueChanges.subscribe((value) => {
        console.log('Name changes', value);
      });
    });
```

# Reactive forms

Compared to Template driven form, Reactive forms are more scalable because this approach doesn't rely on templates. 
This approach, explicitly declares `FormGroup` or `FormControl` in the component file. This way, we can programmatically handle the form validations, update values, reset form state, ...etc.
It is scalable because, everything is handled on the component side, the template can even render the form controls dynamically. So if the form needs update, we just need to update on the component side and leave the template untouched.
Aside from that, Reactive forms are typed, so that we can improve readability and maintainability. Type errors are checked at compile time, provide autocomplete for IDEs, ...etc.

## Usage
```typescript
public personNameControl = new FormControl();
// OR
public formGroup = new FormGroup({
	name: new FormControl(),
	age: new FormControl()
});

ngOnInit(): void {
	this.personNameControl.valueChanges.subscribe((value) => {
		console.log('Name changes', value);
    });
    
	this.formGroup.valueChanges((values) => {
		console.log(values.name, values.age);
	});
}
```

## Data flow
The flow of data in Reactive forms is more straightforward than Template-driven forms
1. The user types a value into the input element, in this case the favorite color _Blue_.
2. The form input element emits an "input" event with the latest value.
3. The `ControlValueAccessor` listening for events on the form input element immediately relays the new value to the `FormControl` instance.
4. The `FormControl` instance emits the new value through the `valueChanges` observable.
5. Any subscribers to the `valueChanges` observable receive the new value.

# Key differences
|                                                                                  | Reactive                             | Template-driven                 |
| :------------------------------------------------------------------------------- | :----------------------------------- | :------------------------------ |
| [Setup of form model](https://angular.dev/guide/forms#setting-up-the-form-model) | Explicit, created in component class | Implicit, created by directives |
| [Data model](https://angular.dev/guide/forms#mutability-of-the-data-model)       | Structured and immutable             | Unstructured and mutable        |
| [Data flow](https://angular.dev/guide/forms#data-flow-in-forms)                  | Synchronous                          | Asynchronous                    |
| [Form validation](https://angular.dev/guide/forms#form-validation)               | Functions                            | Directives                      |

# Form validation
## Template driven forms
We can use validation directive on the template
```html
<input id="name" name="name" type="text" [(ngModel)]="personName" required/>
```

## Reactive forms
We can define validations at the form declaration or add dynamically.
```typescript
actorForm: FormGroup = new FormGroup({ 
	name: new FormControl(this.actor.name, [
		Validators.required, 
		Validators.minLength(4),
		forbiddenNameValidator(/bob/i), // Custom validator
	]),
});

ngOnInit(): void {
	// Add validator using addValidators method
	setTimeout(() => {
		this.actorForm.controls.name.addValidators([...])
	}, 2000);
}
```

