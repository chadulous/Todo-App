<script lang="ts">
    import { deleteTodo, toggleTodoCompleted } from "$lib/stores";
    import { fly } from "svelte/transition";
    import { flip } from "svelte/animate"
    type Todo = {
        text: string,
        completed: boolean,
        id: number
    };
    let input
    $: input = todo.completed
    export let todo: Todo
    export let index: number
</script>
<li class="bg-white flex items-center shadow-sm border border-gray-200 rounded-lg my-2 py-2 px-4" transition:fly={{ x: -200, duration: 200 }}>
    <input type="checkbox" name="completed" bind:checked={input} on:change={() => toggleTodoCompleted(index)} class="mr-2 cursor-pointer form-checkbox h-5 w-5">
    <span class='flex-1 text-gray-800 truncate hover:overflow-x-auto hover:text-clip transition-colors cursor-pointer {todo.completed ? 'text-gray-300' : ''}' on:click={() => toggleTodoCompleted(index)}>
        <span class:strike={todo.completed}>
            {todo.text}
        </span>
    </span>
    <button type="button" class="del" on:click={()=>deleteTodo(index)}>
        <i class="fas fa-minus-square" />
    </button>
</li>