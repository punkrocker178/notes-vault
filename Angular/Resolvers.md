Provide data to the route currently navigating to. Route is activated when data is resolved.
> A data provider can be used with the router to resolve data during navigation. The router waits for the data to be resolved before the route is finally activated.

## Use cases
1. **Separate data layer**: By separate the data retrieval from the component. We can reuse data retrieval anywhere and offload the logic of the component.
2. **Dynamically inject service**: In a growing application, we may have a `BaseService` and `ServiceA` and `ServiceB`, a shared component used in many features. FeatureA needs the component to inject`ServiceA` and FeatureB needs to inject `ServiceB`. To do this, we can use a resolver to resolve the correct service to it's corresponding routes
	Example:
```typescript
// Routing module... or route.ts
routes = [
		{
			path: 'featureA/details/:id', 
			component: FeatureA, 
			resolve: { commonService: ServiceA },
		},
		{
			path: 'featureB/details/:id', 
			component: FeatureB, 
			resolve: { commonService: ServiceB },
		},
	]),
];
```