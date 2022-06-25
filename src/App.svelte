<script>
	import logo from "./assets/svelte.png";
	import AddPersonForm from "./AddPersonForm.svelte";
	//import Counter from "./lib/Counter.svelte";

	let nombre = "Said";
	let firstName = "Jimy";
	let lastName = "Hendrix";
	let colorText = "black";

	// Reactive value: change when the two variables update
	$: fullName = `${firstName} ${lastName}`;

	// Reactive statement
	$: {
		console.log(colorText);
		console.log(fullName);
	}

	const handleClick = () => {
		nombre = "Nahum"
	}

	let people = [
		{ id:1, name: "yoshi", color: "black", age: 25 },
		{ id:2, name: "mario", color: "red", age: 21 },
		{ id:3, name: "luigi", color: "yellow", age: 20 }
	]

	const handleClickDelete = (id) => {
		people = people.filter((person) => person.id != id);
	}

	let hello = true;

	const addPerson = (e) => {
		//console.log(e.detail);
		const person = e.detail;
		people = [person, ...people];
	}

</script>

<main >
	<a href="/">
		<img src={logo} id="loco" alt="Svelte Logo" />
	</a>

	<h2 style="color: {colorText}">{fullName} - {colorText}</h2>

	<!--<button on:click={handleClick} >Update Text Name</button><br><br> -->

	<input type="text" placeholder="Enter first name" bind:value={firstName}>
	<input type="text" placeholder="Enter last name" bind:value={lastName}>
	<input type="text" placeholder="Enter a color" bind:value={colorText}>

	<div class="grid">
		{#each people as person (person.id)}
			<div class:hello={hello}>
				<h4>{person.name}</h4>
				<p>{person.age} years old, <span style="color: {person.color}">{person.color}</span> is prefered color</p>
				<button on:click={ () => handleClickDelete(person.id) }>delete</button>
			</div>
		{:else}
			<h1>There are no people to show ...</h1>
		{/each}
	</div>

	<!-- <Counter /> -->

	<h4 class="red">Red</h4>

	<AddPersonForm on:addPerson={addPerson}/>

</main>

<style>
	:global(body){
		margin: 0;
		padding: 0;
	}

	:root {
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
			Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
	}

	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
		background-color: var(--walpaper-color);
	}

	img {
		height: 16rem;
		width: 16rem;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
		line-height: 1.1;
		margin: 2rem auto;
		max-width: 14rem;
	}

	p {
		max-width: 14rem;
		margin: 1rem auto;
		line-height: 1.35;
	}

	@media (min-width: 480px) {
		h1 {
			max-width: none;
		}

		p {
			max-width: none;
		}
	}

	:global(:root) {
		--walpaper-color: lightblue;
	}

	h4:global(.red){
		color: #ff3e00;
	}

	.hello {
		background-color: lightsalmon;
		padding: 10px;
		border-radius: 20px;
	}

	.grid {
		display: flex;
		justify-content: center;
		gap: 10px; 
		margin: 20px 0px;
	}
</style>
