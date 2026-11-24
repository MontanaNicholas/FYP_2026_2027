
<svelte:head>
	<title>Oh, RATS! | About the Game</title>
</svelte:head>

<div class="page-container">
	<main class="about-screen">

		<a href="/" class="back-button">BACK</a>

		<section class="story-panel">
		

			<p>
                Oh, RATS! is a strategic, top down 2D adventure game where one hungry little rat has its eyes on the ultimate prize: the contents of the fridge!
			</p>

			<p>
				Set inside a house full of winding routes, hidden dangers and tempting hiding spots, you'll need to explore each room, track down the missing fridge key and find your way to the kitchen. 
                But a big hungry cat is on patrol, and getting caught is the last thing you want. 
                With traps to avoid, unexpected encounters and a few tricks to keep up your sleeve, every move could bring you closer to victory… or straight into trouble.
			</p>

			<p>
				Roll the dice, plan your route, and use your combat cards wisely. You'll need a bit of luck, a clever strategy and nerves of steel to make it to that fridge.
			</p>

		</section>

	</main>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(body) {
		margin: 0;
		background: #390b35;
		font-family: Arial, sans-serif;
	}

	.page-container {
		min-height: 100vh;
		min-height: 100svh;
		display: flex;
		justify-content: center;
		background: #390b35;
	}

	.about-screen {
		position: relative;
		width: min(100vw, 66.67svh);
		aspect-ratio: 2 / 3;
		background-image: url('/images/about-game.png');
		background-size: 100% 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	.back-button {
		position: absolute;
		top: 3%;
		left: 5%;
		color: #ffcf60;
		font-weight: bold;
		font-size: 13px;
		text-decoration: none;
	}

	.story-panel {
		position: absolute;
		top: 32%;
		right: 5%;
		width: 47%;
		max-height: 57%;
		overflow-y: auto;
		padding: 5%;
		border: 3px solid #3a123c;
		border-radius: 15px;
		background: #ffebc9;
		color: #390b35;
	}

	.story-panel p {
		font-size: clamp(10px, 1.15vw, 14px);
		line-height: 1.5;
	}


	@media (max-width: 500px) {
		.story-panel {
			border-width: 2px;
			border-radius: 10px;
		}
	}
</style>
