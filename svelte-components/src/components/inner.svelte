<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    function greet() {
        dispatch("greet", "hello");
    }
</script>

<div>
    <button on:click={greet}>Greet</button>
</div>
