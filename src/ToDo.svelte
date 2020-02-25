<script>
    import { fade } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function remove() {
        dispatch('remove', {uid})
    }

	function toggleStatus() {
        let newStatus = !complete;
		dispatch('toggle', {
            uid,
            newStatus
        });
    }

    export let uid;
    export let description;
    export let complete;
</script>

<div class="todo-item" transition:fade="{{delay: 250, duration: 300}}">
    {#if complete}
    <span class="is-complete">{ description }</span>
    <button on:click={toggleStatus}> ✔️ </button>
    {:else}
        <span>{ description }</span>
        <button on:click={toggleStatus}> ❌ </button>
    {/if}
    <button on:click={remove}> 🗑 </button>
</div>

<style>
.todo-item {
    position: relative;
    line-height: 1.2;
    padding: 0.5em 2.5em 0.5em 2em;
    margin: 0 0 0.5em 0;
    border-radius: 2px;
    user-select: none;
    border: 1px solid hsl(240, 8%, 70%);
    background-color: hsl(240, 8%, 93%);
    color: #333;
  }
.is-complete {
    text-decoration: line-through;
    color: green;
}
</style>