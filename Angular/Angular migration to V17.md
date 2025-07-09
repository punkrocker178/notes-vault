#material #swiperjs #migration

# Breaking changes from V14 to V16 (Current project):

- Non MDC Material components are now called as `LegacyComponent`
- Material theming conflicts with MDC components => Need to create a new theme to support both legacy and mdc components (`base-theme.config`)
- Swiper V9 removed Angular Swiper component
- Material sass import errors on CI environment (Solved by reduce global `@angular/material` imports, only import what is needed)

In order to upgrade to V18, we need to migrate all `LegacyComponent` to MDC components (Angular V17 still let us use Material 16, from V18 we will need to sync to Material 18)

# Migrating Legacy Material to MDC Material

> You may also want to migrate your app one module at a time instead of all together. You can use both the old implementation and new implementation in the same application, as long as they aren't used in the same `NgModule`

## Current problem with our project

We are importing Legacy Material modules in a `Shared` module. `Shared` module has many dependencies thus spliting and migrating each MDC module one at a time is very difficult.

## Solutions

- Import both MDC and legacy module. 
	> Failed, will give duplicate component selector error.
- Try wrap each material component by our own component.
 > 	Not feasible as each component has many different inputs that we have to explicitly pass through