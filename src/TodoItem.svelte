<script>
    import {createEventDispatcher} from 'svelte';

    export let id;
    export let name;
    export let completed;

    const dispatch = createEventDispatcher();

    function emitComplete(){
        completed = !completed;
        dispatch('complete', {
            id: id
        })
    }

</script>

<main>
    <div class={completed === true ? 'todoItem completed':'todoItem'} on:click={emitComplete}>
        <input type="checkbox" checked={completed}>
        <p>{name}</p>
    </div>
</main>

<style>

* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

.completed {
    background-color: rgba(95, 255, 47, 0.445);
}

.todoItem {
    display: flex;
    align-items: center;
    max-width: 500px;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 10px;
}

.todoItem > input {
    margin: 0 20px;
    transform: scale(1.8, 1.8);
    border-radius: 10%;
}

.todoItem > p {
    font-size: 25px;
}

</style>