# Comparison with Angular
- `<RouterView>` is similar to `<router-outlet>`
- Text interpolation: Same `{{ //JavaScript code here }}`
- Binding Vue attribute: `v-bind:attribute`. Shorthand: `:attribute`. In Angular we just need square brackets `[attribute]` for Angular to bind
- Directives: Similar to angular structural directives `v-if`, `v-for`
- Content projection: `v-slot` and `slot`
- Styles binding are similar
- `ref()` and `computed()` are similar to Angular Signals. These are reactive getter/setter method that wrap around a value. Vue is able to track this value and update DOM automatically. To listening for `ref` value changes for side effects, we can use `watch` or `watchEffect`
- Form binding: using `reactive()` to create a reactive object, then bind to forms by using `v-model` directive

# Single file components
Vue components file format is `*.vue`. It encapsulates, JavaScript, HTML (template) and styles

Ex:
```vue
<script setup>
 import { ref } from 'vue' 
 const count = ref(0)
</script>

<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped> button { font-weight: bold; } </style>
```

## API Styles
### 1. Option API
Logic is defined as an object containing: `data`, `methods`, `mounted`
### 2. Composition API
Use `<script setup>` to wrap around JavaScript/Typescript code.
> The `setup` attribute is a hint that makes Vue perform compile-time transforms that allow us to use Composition API with less boilerplate.

# Application bootstraping
App bootstrap is similar to React
1. We need to create the root component
2. Then from that root component, we can initialize the application instance `createApp(RootComponent)`
3. In order for the application instance to render the DOM elements, we need to mount the app by calling `app.mount('#app')`. The mounting point is the container for the rendered elements.
