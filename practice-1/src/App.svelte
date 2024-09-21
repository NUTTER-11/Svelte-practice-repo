<script>
	const name = "Batman";
	const channel = "<b>I have Batmobile</b>";
	const hack = `<a href="#" onclick="alert('You are protected by Batman ')">What will happen to you??</a>`;
	const headingid = "heading";
	const id = "headid";
	const disabled = false;
	const status = "success";
	const badstatus = "danger";
	const ispromoted = true;
	const promoted = true;
	const num = "1";
	const names = ["Bruce", "Clark", "Diana"];
	const fullnames = [
		{ firstname: "Bruce", lastname: "Wayne" },
		{ firstname: "Clark", lastname: "Kent" },
		{ firstname: "Princess", lastname: "Diana" },
	];

	let count = 0;

	function handleclick(event, step) {
		console.log(event);
		count += step;
	}

	const formvalues = {
		name: "",
		profilesummary: "",
		country: "",
		joblocation: [],
		remotework: false,
		skill: [],
		experience: "",
	};
	function submitform(event) {
		event.preventDefault();
		console.log(formvalues);
	}

	let firstname = "Bruce";
	let lastname = "Wayne";
	$: fullname = `${firstname} ${lastname}`;

	let items = [
		{ id: 1, title: "Wayne", price: 100 },
		{ id: 2, title: "Kent", price: 200 },
		{ id: 3, title: "Diana", price: 300 },
	];

	$: total = items.reduce((total, curr) => (total = total + curr.price), 0);
	$: {
		console.log(`FullName is ${firstname} ${lastname}`);
	}

	$: {
		const greet = `FullName is ${firstname} ${lastname}`;
		console.log(greet);
	}

	let volume = 0;
	$: if(volume<0){
		alert('Volume cantbe less then 0')
		volume=0
	}else if(volume>100){
		alert('volume cant go heigher')
		volume=100
	}
</script>

<main>
	<h1 class={status}>Here In GOTHAM</h1>
	<h2>I am {name}</h2>
	<div>{@html channel}</div>
	<div>{@html hack}</div>
	<h2 id={headingid}>I have killed Ra's al Ghul</h2>
	<h2 {id}>I have killed Joker</h2>

	<h2 class={badstatus}>I have killed Bane</h2>
	<button {disabled}>You are joking </button>
	<h2 class="undeline">i am joker</h2>
	<h2 class={ispromoted ? "promoted" : ""}>and i am back</h2>
	<h2 class="promoted" {ispromoted}>and i will rule here</h2>
	<h2 class="promoted">and kill batman</h2>

	{#if num === 0}
		<h2>the no is zero</h2>
	{:else if num < 0}
		<h2>the number is less then 0</h2>
	{:else if num > 0}
		<h2>the number is greater then 0</h2>
	{:else}
		<h2>Not a no</h2>
	{/if}

	{#each names as name, index}
		<h2>{index + 1}.{name}</h2>
	{/each}

	{#each fullnames as name, index (name)}
		<h2>{index + 1}.{name.firstname} {name.lastname}</h2>
	{/each}

	<button on:click={() => (count = count + 1)}>Count {count}</button>
	<button on:click={handleclick}>Count {count}</button>
	<button on:click={(event) => handleclick(event, 5)}>Count {count}</button>
	<button on:click={(event) => handleclick(event, 10)}>Count {count}</button>
	<div>
		{JSON.stringify(formvalues, null, 2)}
	</div>
	<form on:submit={submitform}>
		<div>
			<label for="name">Name</label>
			<input type="text" id="name" bind:value={formvalues.name} />
		</div>
		<div>
			<label for="profile">Profile Summary</label>
			<input
				type="text"
				id="profiles"
				bind:value={formvalues.profilesummary}
			/>
		</div>
		<div>
			<label for="country">country</label>
			<select id="country" bind:value={formvalues.country}>
				<option value="">Select a Country</option>
				<option value="india">India</option>
				<option value="Vietnam">Vietnam</option>
				<option value="Singapore">Singapore</option>
			</select>
		</div>
		<div>
			<label for="Job-Location">Job Location</label>
			<select
				id="Job-Location"
				bind:value={formvalues.joblocation}
				multiple
			>
				<option value="">Select a Country</option>
				<option value="india">India</option>
				<option value="Vietnam">Vietnam</option>
				<option value="Singapore">Singapore</option>
			</select>
		</div>
		<div>
			<input
				type="checkbox"
				id="remotework"
				bind:checked={formvalues.remotework}
			/>
			<label for="remotework">Open to remote work</label>
		</div>
		<div>
			<label for="Skill">Skill set</label>
			<input
				type="checkbox"
				id="html"
				value="html"
				bind:group={formvalues.skill}
			/>
			<label for="html">html</label>
			<input
				type="checkbox"
				id="css"
				vslue="css"
				bind:group={formvalues.skill}
			/>
			<label for="css">css</label>
			<input
				type="checkbox"
				id="js"
				value="js"
				bind:group={formvalues.skill}
			/>
			<label for="js">js</label>
		</div>
		<div>
			<label for="experience">Years of Experience</label>
			<input
				type="radio"
				id="0-2"
				value="0-2"
				bind:group={formvalues.experience}
			/>
			<label for="0-2">0-2 years</label>
			<input
				type="radio"
				id="2-4"
				vslue="2-4"
				bind:group={formvalues.experience}
			/>
			<label for="2-4">2-4 years</label>
			<input
				type="radio"
				id="4-8"
				value="4-8"
				bind:group={formvalues.experience}
			/>
			<label for="4-8">4-8 years</label>
		</div>
		<button>Submit</button>
	</form>

	<div>
		<button
			on:click={() => {
				(firstname = "clark"), (lastname = "kent");
			}}
			>onclick Change the name
		</button>
		<h1>{firstname} {lastname}</h1>
		<h2>{fullname}</h2>
		<button
			on:click={() =>
				(items = [...items, { id: 4, title: "keyboard", price: 400 }])}
			>add item in array</button
		>
	</div>
	<div>
		Total - {items.reduce((total, curr) => (total = total + curr.price), 0)}
		totall = {total}
	</div>
	<h1>volume is {volume}</h1>
	<button on:click={()=>(volume+=10)}>Increase volume </button>
	<button on:click={()=>(volume-=10)}>Decrease volume </button>
</main>

<style>
	input + label {
		display: inline-flex;
	}
	.undeline {
		text-decoration: underline;
	}
	.danger {
		color: #ff3e00;
	}
	.success {
		color: olive;
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
	.promoted {
		font-style: italic;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
