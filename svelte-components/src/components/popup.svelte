<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
</script>

<div>
    <h1>This is a pop up</h1>
    <button on:click={() => dispatch('close','bruce')}>close pop-up</button>
</div>
