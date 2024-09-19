<script>
    import { getContext } from "svelte";
    const username = getContext("username-Context");
</script>

<main>
    <h1>this is component e</h1>
    <h2>child f {username}</h2>
</main>
