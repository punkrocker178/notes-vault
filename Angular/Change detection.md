A mechanism that check all components properties for changes and updating the view(DOM) after an async tasks or browser APIs call.
There are 2 change detection strategies:
- **Default:** Checks all components and their bindings after any event or async operation.
- **On Push:**  Only checks a component when its `@Input` properties change by reference or when the developer explicitly signals a change. Result in reduced unnecessary detection cycles.

**Note:** Should use `OnPush` strategy along side with `signals` or `Observables` to let Angular automatically handle the UI updates. Otherwise we have to manually run change detection.

We can manually interact with the change detection system using methods from the `ChangeDetectorRef`: 
- `markForCheck()`:  Signals Angular to check the component for changes.
- `detach()`: Excludes the component from change detection until re-attached.
- `detectChanges()`: Manually checks the component and children.
- `checkNoChanges()`: Throws an error if unexpected changes are detected
# Zone.js
[Angular zone.js](https://github.com/angular/angular/tree/main/packages/zone.js) library is built to track browser API and async tasks completion. Zone.js mechanism is wrapping JavaScript code and executing it in a specific context or zone (Patch browser API). 
In Angular, Zone.js is used to create a new zone for each component and to track changes within that component’s zone. If there are changes in a zone, it will notify to Angular to begin change detection and update view if necessary.

# NgZone
Is built on top of Zone.js to manage excution context to directly perform change detections. It exposes APIs that let Angular developers run code inside or outside the "Angular zone" to control when change detection is triggered.
The ability to manually control the change detection triggers will prevent unnecessary detections cylces caused by heavy tasks that don't need to update view.
## Examples
### 1. Running Code Inside the Angular Zone
Use `ngZone.run()` to ensure Angular detects changes resulting from code outside its zone, such as after a third-party library triggers a state update.[](https://mallikarjun.hashnode.dev/ngzone-and-change-detection-in-angular)

```typescript
import { Component, NgZone } from '@angular/core'; 
@Component({   // ... }) 
export class MyComponent {   
	constructor(private ngZone: NgZone) {}   
	updateData() {     
		this.ngZone.run(() => {       
			// Any code here triggers change detection       
			this.data = 'Updated!';     
		});   
	} 
}
```

## 2. Running Code Outside the Angular Zone
Use `ngZone.runOutsideAngular()` to execute code that should not trigger Angular's change detection. This is ideal for performance-heavy tasks such as event listeners or animations. See [Zone pollution](https://angular.dev/best-practices/zone-pollution)
```typescript
startHeavyTask() {   
	this.ngZone.runOutsideAngular(() => {     
	// Intensive computations, listeners, etc.
	setTimeout(() => {       
	// When you want to update Angular, get back in the zone if needed:       
		this.ngZone.run(() => {         
			this.data = 'Done!';       
		});    
	}, 1000);   
}); 
}
```