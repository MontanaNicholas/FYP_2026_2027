<script>
	import { onMount } from 'svelte';

	let health = $state(10);
	let trapTriggered = $state(false);
	let trap = $state(null);

	onMount(() => {
		trap = new URLSearchParams(window.location.search).get('trap');

		if (trap) {
			activateTrap();
		}
	});

	function activateTrap() {
		health = health - 5;
		trapTriggered = true;
	}
</script>

<div class="body-container">

	<h1>OH, RATS!</h1>

	<h2>Rat Player</h2>

	{#if trap}
		<p>Trap identified!</p>
	{/if}
	
	<div class="health">
		{health} / 10 HP
	</div>

	<div class="trap">
		<h2>Trap</h2>

		<p>Damage: -5 HP</p>

		<button onclick={activateTrap} disabled={trapTriggered}>
			Activate Trap
		</button>

		{#if trapTriggered}
			<p>Trap triggered! Rat lost 5 HP.</p>
		{/if}
	</div>

</div>

<style>
	:global(body) {
		font-family: Arial, sans-serif;
		background: #f4efe6;
		margin: 0;
	}

	.body-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 2rem;
		min-height: 100vh;
	}

	h1 {
		text-align: center;
		margin-top: 40px;
	}

	h2 {
		text-align: center;
	}

	.health {
		width: 250px;
		margin: 30px auto;
		padding: 20px;
		background: white;
		border-radius: 12px;
		text-align: center;
		font-size: 24px;
		font-weight: bold;
	}

	.trap {
		width: 300px;
		margin: 30px auto;
		padding: 25px;
		background: white;
		border-radius: 12px;
		text-align: center;
	}

	button {
		padding: 12px 20px;
		font-size: 16px;
		cursor: pointer;
		border: none;
		border-radius: 8px;
	}
</style>