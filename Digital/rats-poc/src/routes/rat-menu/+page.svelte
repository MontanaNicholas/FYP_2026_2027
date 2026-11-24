
<svelte:head>
	<title>Oh, RATS! | Rat Menu</title>
</svelte:head>

<div class="page-container">
	<main class="rat-screen">

		<nav class="menu-buttons">
			<a href="/movement" class="menu-button play-button">
				PLAY
			</a>

			<a href="/how-to-play" class="menu-button">
				HOW TO PLAY
			</a>
		</nav>

		<a href="/" class="back-button"> BACK</a>

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
		overflow: hidden;
	}

	.rat-screen {
		position: relative;
		width: min(100vw, 66.67svh);
		aspect-ratio: 2 / 3;
		background-image: url('/images/rat-character.png');
		background-size: 100% 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	.menu-buttons {
		position: absolute;
		top: 39%;
		right: 8%;
		width: 38%;
		display: flex;
		flex-direction: column;
		gap: 24px;
	}

	.menu-button {
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 13px 8px;
		border: 3px solid #260b2c;
		border-radius: 18px;
		background: #ffcf60;
		color: #390b35;
		font-weight: 900;
		font-size: clamp(11px, 1.4vw, 17px);
		text-decoration: none;
		text-align: center;
		box-shadow: 0 4px 0 #a94b40;
		transition: transform 0.2s, background 0.2s;
	}

	.menu-button:hover {
		transform: scale(1.05);
		background: #ffe39a;
	}

	.play-button {
		background: #ffcf60;
	}

	.back-button {
		position: absolute;
		top: 3%;
		left: 5%;
		color: #ffe5bd;
		font-weight: bold;
		text-decoration: none;
		font-size: 14px;
	}

	@media (max-width: 500px) {
		.menu-button {
			padding: 9px 5px;
			border-width: 2px;
			border-radius: 12px;
		}

		.menu-buttons {
			gap: 11px;
		}
	}
</style>
