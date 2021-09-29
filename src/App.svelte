<script>
	import ContactCard from './ContactCard.svelte'

	export let name
	let job = ""
	let description = ""
	let userImg = ""
	let age = 24

	$: upperCaseName = name.toUpperCase()

	$: console.log(name);

	$: if (name === 'Maximilian') {
		age = 31
	}


	function incrementAge() {
		age +=1
	}

	function nameInput(event) {
		const enteredValue = event.target.value
		name = enteredValue
	}
</script>

<style>
	h1 {
		color: purple;
	}

	span {
		color: rosybrown;
	}
</style>

<h1>Hello {upperCaseName}, my age is <span>{age}</span> yo!</h1>
<button on:click="{incrementAge}">Change Age +</button>
<!-- <button on:click="{changeName}">Change Name</button> -->
<!-- <input type="text" value="{name}" on:input="{nameInput}"/> -->
<input type="text" bind:value="{name}" />
<input type="text" bind:value="{job}" />
<input type="text" bind:value="{userImg}" />
<textarea type="text" rows='3' bind:value="{description}" />


<ContactCard 
	userName={name}
	userJob={job}
	userDescription={description}
	{userImg}
/>