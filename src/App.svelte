<script>
	import TodoItem from "./TodoItem.svelte";

	let hideFinished = false;
	let newTodo = '';

	let todoList = [{
		id: 0,
		name: "Buy milk1",
		completed: true
	}, {
		id: 1,
		name: "Buy milk2",
		completed: false
	}, {
		id: 2,
		name: "Buy milk3",
		completed: true
	}, {
		id: 3,
		name: "Buy milk4",
		completed: false
	}]

	function handleHideFinished() {
		hideFinished = !hideFinished;
	}

	function addNewTodo(){
		if (newTodo !== "") {
			todoList = [...todoList, {id: todoList.length, name: newTodo, completed: false}];
			newTodo = ""
			return
		}

		alert("Write a todo to be added fisrt")
	}

	function handleComplete(event){
		todoList[event.detail.id].completed = !todoList[event.detail.id].completed
	}

</script>

<main>
	<h1>Todo List App</h1>
	
	<form class="form" on:submit|preventDefault={addNewTodo}>
		<label for="add-todo">Add a todo item</label>
		<input bind:value={newTodo} type="text" name="add-todo" placeholder="Enter a new todo item">
		<button>Submit</button>
	</form>
	
	<input type="button"
	on:click|preventDefault={handleHideFinished}
	value={hideFinished === true ? 'Show completed tasks': 'Hide completed tasks'}
	/>

	<ul class="todo-list">
		{#each todoList as item}
			{#if hideFinished && !item.completed}
				<TodoItem on:complete={handleComplete} {...item} />
			{:else if !hideFinished}
				<TodoItem on:complete={handleComplete} {...item} />
			{/if}
		{:else}
			<h3>Nothing appears...</h3>
		{/each}
	</ul>
</main>

<style>

* {
	font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

.todo-list {
	padding: 0;
}

</style>