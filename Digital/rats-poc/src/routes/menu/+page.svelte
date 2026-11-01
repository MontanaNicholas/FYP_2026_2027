
<script>
	let playerSide = '';

	// Get the selected character
	if (typeof window !== 'undefined') {
		playerSide = localStorage.getItem('playerSide') || '';
	}
</script>

<svelte:head>
	<title>OH, RATS! - Main Menu</title>
</svelte:head>

<div class="page-container">
	<main>
		<div class="title-section">
			<p class="welcome">WELCOME BACK!</p>
			<h1>OH, RATS!</h1>
		</div>

		<div class="player-info">
			<p>YOU ARE PLAYING AS</p>
			<h2>{playerSide === 'cat' ? 'THE CAT' : 'THE RATS'}</h2>
		</div>

		<div class="menu-section">
			<h2>MAIN MENU</h2>

			<div class="menu-options">
				<a href="/movement" class="menu-button play">
					<span class="button-icon">▶</span>
					<span>PLAY GAME</span>
				</a>

				<a href="/rules" class="menu-button rules">
					<span class="button-icon">?</span>
					<span>HOW TO PLAY</span>
				</a>

				<a href="/about" class="menu-button about">
					<span class="button-icon">★</span>
					<span>ABOUT THE GAME</span>
				</a>
			</div>
		</div>

		<a href="/" class="back-link">← CHANGE CHARACTER</a>
	</main>
</div>

<style>
	:global(body) {
		margin: 0;
		font-family: Arial, sans-serif;
		background: #19172D;
		color: #FFF2D7;
	}

	.page-container {
		min-height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 30px 20px;
		box-sizing: border-box;
	}

	main {
		width: 100%;
		max-width: 600px;
		text-align: center;
	}

	.title-section {
		margin-bottom: 30px;
	}

	.welcome {
		font-size: 13px;
		letter-spacing: 4px;
		color: #F5DDA8;
	}

	h1 {
		font-size: clamp(55px, 12vw, 85px);
		margin: 15px 0;
		font-weight: 900;
		letter-spacing: 3px;
	}

	.player-info {
		margin: 30px auto;
		padding: 15px;
		max-width: 260px;
		border: 2px solid #77658F;
		border-radius: 12px;
	}

	.player-info p {
		font-size: 11px;
		letter-spacing: 2px;
		color: #C5B7D9;
		margin: 0 0 8px;
	}

	.player-info h2 {
		margin: 0;
		font-size: 23px;
		color: #F5DDA8;
	}

	.menu-section h2 {
		font-size: 22px;
		letter-spacing: 2px;
		margin-bottom: 20px;
	}

	.menu-options {
		display: flex;
		flex-direction: column;
		gap: 14px;
	}

	.menu-button {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 15px;
		padding: 20px;
		border-radius: 12px;
		text-decoration: none;
		font-size: 18px;
		font-weight: bold;
		letter-spacing: 1px;
		transition: transform 0.2s, filter 0.2s;
	}

	.menu-button:hover {
		transform: translateY(-4px);
		filter: brightness(1.1);
	}

	.play {
		background: #E8D4A9;
		color: #49372C;
	}

	.rules {
		background: #C6B7D9;
		color: #382C49;
	}

	.about {
		background: #A9C6B5;
		color: #263F34;
	}

	.button-icon {
		font-size: 22px;
	}

	.back-link {
		display: inline-block;
		margin-top: 35px;
		color: #C5B7D9;
		font-size: 12px;
		letter-spacing: 1px;
		text-decoration: none;
	}

	.back-link:hover {
		color: #FFF2D7;
	}

	@media (max-width: 480px) {
		.title-section {
			margin-bottom: 20px;
		}

		.menu-button {
			padding: 18px;
			font-size: 16px;
		}
	}
</style>
