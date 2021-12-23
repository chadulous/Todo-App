<script lang="ts">
    import FormError from '$lib/components/FormError.svelte';
    let ferror: FormError
    let todo = '';
    import { addTodo } from '$lib/stores';
    const handleSubmit = () => {
        if(todo.length === 0) error()
        addTodo(todo)
        todo = ''
        console.log("submitting")
    }
    let input: HTMLInputElement
    const error = ()=>{
        ferror.on('Todo name cannot be blank')
        input.classList.add('error')
        setTimeout(()=>{
                ferror.off()
                input.classList.remove('error')
            }, 5e3)
        throw new Error('input cannot be blank')
    }
</script>
<form class="my-6" on:submit|preventDefault={handleSubmit} autocomplete="off">
    <div class="flex flex-col text-sm mb-2">
        <label class="font-bold mb-2 text-gray-800" for="todo">
            <p>Todo:</p>
        </label>
        <input type="text" name="todo" bind:value={todo} bind:this={input} placeholder="What do you need to do?" class="transition-colors appearance-none shadow-sm border border-gray-200 p-2 focus:outline-none focus:border-gray-400 hover:border-gray-300 rounded-lg" id="todo">
        <FormError bind:this={ferror}></FormError>
    </div>
    <!-- <button type="submit" class="w-full shadow-sm rounded bg-blue-500 hover:bg-blue-600 text-white py-2 px-4 transition-colors">Submit</button> -->
    <hr>
</form>