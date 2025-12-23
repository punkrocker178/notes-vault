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

# API Styles
## 1. Option API
Component logic is defined as an object containing: `data`, `methods`, `mounted`
```vue
<script>
export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {
    return {
      count: 0
    }
  },
  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event handlers in templates.
  methods: {
    increment() {
      this.count++
    }
  },
  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

## 2. Composition API
Component logic is defined similar to block level JavaScript code. With the use of `<script setup>` in order to import API functions.
> The `setup` attribute is a hint that makes Vue perform compile-time transforms that allow us to use Composition API with less boilerplate.

```vue
<script setup>
import { ref, onMounted } from 'vue'
// reactive state
const count = ref(0)
// functions that mutate state and trigger updates
function increment() {
  count.value++
}
// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

# Lifecycle hooks
## Notable clientSide hooks
- `onMounted`:  callback function is called after component is mounted. Component is mounted when all synchronous child components are mounted and it's DOM tree is inserted to parent.
- `onUpdated`: callback function is called when there are any DOM update of the component.
- `onUnmounted`: callback function is called when component is unmounted. Meaning, all of the child components are unmounted and associated effects are stopped.

## Diagram
![Vue lifecycle diagram](https://vuejs.org/assets/lifecycle.MuZLBFAS.png)
