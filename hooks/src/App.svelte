<script>
	import Postlist from "./components/postlist.svelte";
	import AutoFocus from "./components/AutoFocus.svelte";
	import Taba from "./components/Taba.svelte";
	import Tabb from "./components/Tabb.svelte";
	import Tabc from "./components/Tabc.svelte";
	import Counter, { getTotalcount } from "./components/counter.svelte";
	export let name;
	let activetab = Taba;
</script>

<main>
	<h1>Hello {name}!</h1>
	<!-- <button on:click={() => (activetab = "Taba")}>Tab A</button>
	<button on:click={() => (activetab = "Tabb")}>Tab B</button>
	<button on:click={() => (activetab = "Tabc")}>Tab c</button> -->
	<!-- {#if activetab === "Taba"}
		<Taba />
	{/if}
	{#if activetab === "Tabb"}
		<Tabb />
	{/if}
	{#if activetab === "Tabc"}
		<Tabc />
	{/if} -->

	<button on:click={() => (activetab = Taba)}>Tab A</button>
	<button on:click={() => (activetab = Tabb)}>Tab B</button>
	<button on:click={() => (activetab = Tabc)}>Tab c</button>
	<svelte:component this={activetab}></svelte:component>
	<button on:click={() => alert(getTotalcount())}>alret</button>
	<Counter />
	<Counter />
	<Counter />
	<h4>focus</h4>

	<AutoFocus />

	<Postlist></Postlist>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
