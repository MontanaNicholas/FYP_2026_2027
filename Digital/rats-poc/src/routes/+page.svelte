
<script>
</script>

<svelte:head>
	<title>Oh, RATS! | Home</title>
	<meta
		name="description"
		content="Welcome to Oh, RATS! Can you outsmart the cat and reach the fridge?"
	/>
</svelte:head>

<div class="page-container">
	<main class="home-screen">

		<a class="fridge-button setup-button" href="/rat-menu">
			GET SET UP
		</a>

		<a class="fridge-button about-button" href="/about">
			ABOUT THE GAME
		</a>

	</main>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(body) {
		margin: 0;
		background: #260b2c;
		font-family: Arial, sans-serif;
	}

	.page-container {
		min-height: 100vh;
		min-height: 100svh;
		display: flex;
		align-items: center;
		justify-content: center;
		background: #260b2c;
		overflow: hidden;
	}

	.home-screen {
		position: relative;
		width: min(100vw, 66.67svh);
		aspect-ratio: 2 / 3;
		background-image: url('/images/home-screen.png');
		background-size: 100% 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	.fridge-button {
		position: absolute;
		left: 12%;
		width: 21%;
		min-height: 4%;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 4px 3px;
		border: 2px solid #3a123c;
		border-radius: 13px;
		background: #ffcf60;
		color: #3a123c;
		font-weight: 900;
		font-size: clamp(7px, 0.9vw, 11px);
		text-align: center;
		text-decoration: none;
		box-shadow: 0 3px 0 #a94b40;
		transition: transform 0.2s, background 0.2s;
	}

	.fridge-button:hover {
		transform: scale(1.05);
		background: #ffe39a;
	}

	.fridge-button:active {
		transform: translateY(3px);
		box-shadow: none;
	}

	.setup-button {
		top: 55%;
	}

	.about-button {
		top: 63%;
	}

	@media (max-width: 500px) {
		.fridge-button {
			border-width: 2px;
			border-radius: 10px;
			padding: 3px 2px;
			font-size: 7px;
		}
	}
</style>