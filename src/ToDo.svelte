<script>
    export let task;
    import { fade } from 'svelte/transition';

    
</script>

<div class="task-container">
    <h4 transition:fade="{{delay: 250, duration: 300}}">{task}</h4>
</div>