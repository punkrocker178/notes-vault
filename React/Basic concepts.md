## **Components**
Components are function based. Can be exported to be used in other components.

```jsx
export const TodoList = () => {
	return (
		<div>Todo list component</div>
		<TodoItem></TodoItem>
	);
}

export function TodoItem() {
	return (
		<h2>Task 1</h2>
	);
}
```

### Passing props
States declared in parent component can be pass to child component to share data is called `props`.
We pass `props` similar to HTML `attributes`

```jsx
export const TodoList = () => {
	const [itemTitle, setItemTitle] = useState('');
	
	return (
		<div>Todo list component</div>
		<TodoItem title={itemTitle}></TodoItem>
	);
}
```
#### Declaring props
In order for child component to read `props`, it has to be declared.

```jsx
export function TodoItem({ title }) {
	return (
		<h2>{ title }</h2>
	);
}
```