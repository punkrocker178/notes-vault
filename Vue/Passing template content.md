# Slot
We can access template content of a component by using `<slot>` as an outlet for template content.
![Slot example](https://vuejs.org/assets/slots.CKcE8XYd.png)
Rendered DOM:
```html
<button class="fancy-btn">Click me!</button>
```

# Fallback content
By passing the content between `<slot>`. It will behave as a fallback content if component doesn't have template content.
```html
<button type="submit">
  <slot>
    Submit <!-- fallback content -->
  </slot>
</button>
```

# Named slots
By naming slots, we can hold multiple templates and have different outlets for it.
![Named slot example](https://vuejs.org/assets/named-slots.CCIb9Mo_.png)
Example:
Parent template
```html
<BaseLayout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>
  <template #default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>
  <template #footer>
    <p>Here's some contact info</p>
  </template>
</BaseLayout>
```

BaseLayout component template
```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```
