<script>
    import Signup from "./components/signup.svelte";

	const formvalues = {
		name: "",
		email: "",
		gender: "",
		phoneno: "",
		password: "",
		repassword: "",
	};
	function signedup(event){
		event.preventDefault();
		console.log(formvalues)
	}
</script>

<main>
	<Signup></Signup>
	<form on:submit={signedup}>
		<h1>Sign-Up</h1>
		<div>
			<label for='name'>Name</label>
			<input type='text' id='name' bind:value={formvalues.name}/>
		</div>
		<div>
			<label for='email'>E-mail</label>
			<input type='email' id='email' bind:value={formvalues.email}/>
		</div>
		<div>
			<label for='phoneno'>Phone Number</label>
			<input type='number' id='phoneno' bind:value={formvalues.phoneno}/>
		</div>
		<div>
			<label for='gender'>Gender</label>
			<input type='radio' id='male' value="male" bind:group={formvalues.gender}/>
			<label for='male'>Male</label>
			<input type='radio' id='female' value="female" bind:group={formvalues.gender}/>
			<label for='female'>Female</label>
		</div>
		<div>
			<label for='password'>Password</label>
			<input type='password' id='password' bind:value={formvalues.password}/>
		</div>
		<div>
			<label for='repassword'>Re-Password</label>
			<input type='password' id='repassword' bind:value={formvalues.repassword}/>
		</div>
		<button>Sign-up</button>
	</form>
</main>

<style>
		input + label {
		display: inline-flex;
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
