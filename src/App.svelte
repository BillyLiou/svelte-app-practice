<script>
	export let name;
	name = 'Billy';
	let arrs = [1,2,3]
	let bool = false
	let count = 0;
	$: showCount = count;

	function clickCount() {
		count += 1;
	}

	let username;
	let userpassword;
	let email;
	let full_name;
	let result;
	$: showResult = result;
	async function doPost() {
		const res = await fetch('http://127.0.0.1:8000/login',{
			headers: {
				'Access-Control-Allow-Origin': '*'
			},
			// mode: 'cors',
			method: 'POST',
			body: JSON.stringify({
				"username": username,
    			"userpassword": userpassword,
    			"email": email,
    			"full_name" : full_name
			})
		})
		const json = await res.json();
		result = JSON.stringify(json)
	}
	
</script>

<main>
	<!-- <h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	{#each arrs as arr}
		<p>{arr}</p>
	{/each}
	{#if bool}
		<p>判斷boolean為true</p>
	{:else if bool==false}
		<p>判斷boolean為false</p>
	{/if}
	<button on:click={clickCount}>
		點我加一下
	</button>
	<p>{showCount}</p> -->

	<input bind:value={username}>
	<input bind:value={userpassword}>
	<input bind:value={email}>
	<input bind:value={full_name}>
	<button type="button" on:click={doPost}>
		點擊訪問api
	</button>
	<pre>res: {result} </pre>

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