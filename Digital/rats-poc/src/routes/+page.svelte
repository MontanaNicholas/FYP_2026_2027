
<script>
	/** @param {'rat' | 'cat'} side */
function selectSide(side) {
		localStorage.setItem('playerSide', side);

		// Going to the main menu
		window.location.href = '/menu';
	}
</script>

<div class="page-container">

	<main>
		<div class="title-section">
			<p class="welcome">WELCOME TO</p>

			<h1>OH, RATS!</h1>

		</div>

		<div class="selection-section">
			<h2>CHOOSE YOUR SIDE</h2>

			<div class="character-options">

				<button class="character-card rat" onclick={() => selectSide('rat')}>
					<div class="character-image">RAT</div>

					<h3>THE RATS</h3>

					<span>SELECT RAT</span>
				</button>

				<button class="character-card cat" onclick={() => selectSide('cat')}>
					<div class="character-image">CAT</div>

					<h3>THE CAT</h3>

					<span>SELECT CAT</span>
				</button>

			</div>
		</div>

		<p class="footer-text">CHOOSE YOUR CHARACTER TO CONTINUE</p>
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
		max-width: 650px;
		text-align: center;
	}

	.title-section {
		margin-bottom: 55px;
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
		color: #FFF2D7;
	}

	.selection-section h2 {
		font-size: 25px;
		margin-bottom: 8px;
	}

	.selection-section > p {
		color: #C5B7D9;
		margin-bottom: 30px;
	}

	.character-options {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 18px;
	}

	.character-card {
		border: none;
		border-radius: 14px;
		padding: 25px 15px;
		cursor: pointer;
		font-family: inherit;
		transition: transform 0.2s, filter 0.2s;
	}

	.character-card:hover {
		transform: translateY(-5px);
		filter: brightness(1.05);
	}

	.rat {
		background: #E8D4A9;
		color: #49372C;
	}

	.cat {
		background: #C6B7D9;
		color: #382C49;
	}

	.character-image {
		font-size: 30px;
		font-weight: bold;
		margin: 15px 0;
	}

	.character-card h3 {
		font-size: 20px;
	}

	.character-card span {
		display: inline-block;
		margin-top: 15px;
		font-weight: bold;
		font-size: 13px;
		letter-spacing: 1px;
	}

	.footer-text {
		margin-top: 40px;
		font-size: 11px;
		letter-spacing: 2px;
		color: #BDB0CF;
	}

	@media (max-width: 480px) {
		.title-section {
			margin-bottom: 40px;
		}

		.character-options {
			grid-template-columns: 1fr;
			gap: 14px;
		}

		.character-card {
			padding: 18px;
		}

		.character-image {
			margin: 5px 0;
		}


	}
</style>
