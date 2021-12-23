<script lang="ts">
    import Todo from "$lib/components/Todo.svelte";
    import TodoForm from "$lib/components/TodoForm.svelte";
    import { todos } from '$lib/stores';
    import { onMount } from "svelte";
    import { flip } from "svelte/animate";
    onMount(()=>{
        const json = localStorage.getItem('store');
        if (json) {
           todos.set(JSON.parse(json));
        }
      
        todos.subscribe(current => {
            localStorage.setItem('store', JSON.stringify(current));
        });
    })
</script>

<main>
    <h1 class="text-2xl font-bold text-center text-gray-800 md:text-3xl">
        Todo List
    </h1>
    <TodoForm></TodoForm>
    {#each $todos as todo (todo.id)}
        <div animate:flip>
            <Todo todo={todo} index={todo.id}/>
        </div>
    {/each}
</main>