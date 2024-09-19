<script>
	import { setContext } from "svelte";
	import Componentc from "./components/componentc.svelte";
	import Greet from "./components/Greet.svelte";
	import Popup from "./components/popup.svelte";
	import Outer from "./components/outer.svelte";
	import Card from "./components/card.svelte";
	import NameList from "./components/NameList.svelte";
	import Childstyles from "./components/Childstyles.svelte";
	const name = "clark";
	const heroname = "Superman";
	const obj = {
		name: "barry",
		heronames: "flash",
	};
	const username = "batup";
	setContext("username-Context", username);

	let showpopup = false;
	function closepopup(event) {
		(showpopup = false), console.log(event.detail);
	}
	function handlegreet(event) {
		alert(event.detail);
	}
</script>

<main>
	<Greet name="Bruce" heronames="Batman" />
	<Greet {name} heronames={heroname} />
	<Greet name={obj.name} heronames={obj.heroname} />
	<Greet {...obj} />

	<h1>{username}</h1>
	<Componentc></Componentc>
	<button on:click={() => (showpopup = true)}>show popup</button>
	{#if showpopup}
		<!-- <Popup on:close={()=>(showpopup=false)}/> -->
		<Popup on:close={closepopup} />
	{/if}

	<div>
		<Outer on:greet={handlegreet}></Outer>
	</div>
	<!-- <Card content='cardy'></Card>
	<Card content='cardying'></Card> -->
	<!-- <Card>hello</Card>
	<Card><h1>hello</h1></Card> -->
	<NameList>
		<h3 slot="hero" let:firstname let:lastname>{firstname} {lastname}</h3>
	</NameList>

	<Card>
		<div slot="header">hi</div>
		<div slot="content">heloooo</div>
		<hr />
		<!-- {#if $$slots.footer} -->
		<div slot="footer">bye</div>
	</Card>

	<h4>hello ji</h4>
	<h2>hello ji</h2>
	<Childstyles></Childstyles>
</main>

<style>
	:global(h2){
		color: chartreuse;
	}
	h4 {
		color: rgb(45, 179, 19);
	}
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
