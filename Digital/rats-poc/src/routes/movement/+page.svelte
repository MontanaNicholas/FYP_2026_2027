
<script>
	let roll = $state(0);
	let isRolling = $state(false);

	// Rat's starting position
	let ratRow = $state(4);
	let ratCol = $state(0);

	// Key's position
	const keyRow = 1;
	const keyCol = 3;

	let keyCollected = $state(false);

	let message = $state('Roll the dice to begin!');

	// Roll the dice
	function rollDice() {
		if (isRolling || roll > 0 || keyCollected) return;

		isRolling = true;

		setTimeout(() => {
			roll = Math.floor(Math.random() * 6) + 1;
			isRolling = false;
			message = `You rolled a ${roll}! Choose a highlighted tile.`;
		}, 700);
	}

	// Check whether a tile is within movement range
	/** @param {number} row @param {number} col */
	function isReachable(row, col) {
		const distance =
			Math.abs(row - ratRow) + Math.abs(col - ratCol);

		return roll > 0 && distance > 0 && distance <= roll;
	}

	// Move the Rat to a selected tile
	/** @param {number} row @param {number} col */
	function moveRat(row, col) {
		if (!isReachable(row, col)) return;

		ratRow = row;
		ratCol = col;

		// Check if the Rat has found the key
		if (ratRow === keyRow && ratCol === keyCol) {
			keyCollected = true;
			message = 'You found the key! Now get to the fridge!';
		} else {
			message = 'Move complete! Roll the dice for your next turn.';
		}

		// Reset the dice for the next turn
		roll = 0;
	}
</script>

<svelte:head>
	<title>Gameplay | Oh, RATS!</title>
</svelte:head>

<div class="game-page">

	<header>
		<a href="/" class="quit-button">QUIT</a>

		<h1>OH, RATS!</h1>
		<p class="turn-label">RAT 1'S TURN</p>
	</header>

	<div class="info-bar">
		<div class="info-box">
			<span>KEY LOCATION</span>
			<strong>TEST ROOM</strong>
		</div>

		<div class="info-box">
			<span>OBJECTIVE</span>
			<strong>{keyCollected ? 'KEY FOUND!' : 'FIND THE KEY'}</strong>
		</div>
	</div>

	<main>
		<div class="game-layout">

			<!-- BOARD AREA -->
			<div class="board-area">
				<h2>THE ROOM</h2>

				<p class="message">{message}</p>

				<!-- 5 x 5 game board -->
				<div class="board">

					{#each Array.from({ length: 25 }, (_, i) => i) as tile}
						{@const row = Math.floor(tile / 5)}
						{@const col = tile % 5}
						{@const isRat = ratRow === row && ratCol === col}
						{@const isKey = keyRow === row && keyCol === col && !keyCollected}
						{@const canMove = isReachable(row, col)}

						<button
							class="tile"
							class:reachable={canMove}
							class:rat-tile={isRat}
							class:key-tile={isKey}
							disabled={!canMove}
							onclick={() => moveRat(row, col)}
							aria-label={`Tile ${row + 1}, ${col + 1}`}
						>
							{#if isRat}
								<img
									src="/images/RAT_FRONT.png"
									alt="Rat character"
									class="rat-sprite"
								/>
							{/if}

							{#if isKey}
								<img
									src="/images/KEY_TESTER.png"
									alt="Key"
									class="key-sprite"
								/>
							{/if}
						</button>
					{/each}

				</div>
			</div>

			<!-- DICE AREA -->
			<section class="dice-section">

				{#if roll === 0}
					<h2>ROLL THE DICE</h2>
				{:else}
					<h2>YOU ROLLED A {roll}!</h2>
					<p>Choose a highlighted tile to move.</p>
				{/if}

				<svg
					viewBox="0 0 120 120"
					class="dice"
					class:rolling={isRolling}
					role="img"
					aria-label="Dice showing {roll || 1}"
				>
					<defs>
						<linearGradient id="diceColour" x1="0" y1="0" x2="1" y2="1">
							<stop offset="0%" stop-color="#FFF8E9" />
							<stop offset="100%" stop-color="#E8D9BD" />
						</linearGradient>
					</defs>

					<rect
						x="10"
						y="10"
						width="100"
						height="100"
						rx="18"
						fill="url(#diceColour)"
						stroke="#B9A98E"
						stroke-width="2"
					/>

					{#if roll === 0 || roll === 1 || roll === 3 || roll === 5}
						<circle cx="60" cy="60" r="7" fill="#49372C" />
					{/if}

					{#if roll >= 2}
						<circle cx="36" cy="36" r="7" fill="#49372C" />
						<circle cx="84" cy="84" r="7" fill="#49372C" />
					{/if}

					{#if roll === 4 || roll === 5 || roll === 6}
						<circle cx="84" cy="36" r="7" fill="#49372C" />
						<circle cx="36" cy="84" r="7" fill="#49372C" />
					{/if}

					{#if roll === 6}
						<circle cx="36" cy="60" r="7" fill="#49372C" />
						<circle cx="84" cy="60" r="7" fill="#49372C" />
					{/if}
				</svg>

				<button
					class="roll-button"
					onclick={rollDice}
					disabled={isRolling || roll > 0 || keyCollected}
				>
					{#if isRolling}
						ROLLING...
					{:else if roll > 0}
						CHOOSE A TILE
					{:else}
						ROLL DICE
					{/if}
				</button>

				{#if keyCollected}
					<p class="success-message">KEY COLLECTED!</p>
				{/if}

			</section>

		</div>
	</main>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(body) {
		margin: 0;
		font-family: Arial, sans-serif;
		background: #3b0936;
		color: #fff2d7;
	}

	.game-page {
		min-height: 100vh;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 20px;
	}

	header {
		text-align: center;
		margin-bottom: 20px;
	}

	header h1 {
		font-size: 30px;
		margin: 0 0 5px;
		color: #ffcf59;
	}

	.quit-button {
		position: absolute;
		top: 20px;
		left: 20px;
		padding: 9px 18px;
		background: #ffcf59;
		color: #3b0936;
		border: 2px solid #e985dc;
		border-radius: 8px;
		font-size: 13px;
		font-weight: bold;
		text-decoration: none;
		letter-spacing: 1px;
	}

	.quit-button:hover {
		background: #ffe39a;
	}

	.turn-label {
		font-size: 13px;
		letter-spacing: 2px;
		margin: 0;
	}

	.info-bar {
		width: 100%;
		max-width: 500px;
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 12px;
		margin-bottom: 25px;
	}

	.info-box {
		background: #572052;
		border: 2px solid #805080;
		border-radius: 10px;
		padding: 12px 5px;
		text-align: center;
		display: flex;
		flex-direction: column;
		gap: 5px;
	}

	.info-box span {
		font-size: 10px;
		letter-spacing: 1px;
	}

	.info-box strong {
		font-size: 14px;
	}

	/* Main game layout */
	main {
		width: 100%;
		display: flex;
		justify-content: center;
		text-align: center;
	}

	.game-layout {
		width: 100%;
		max-width: 850px;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 40px;
	}

	.board-area {
		flex: 0 1 500px;
		min-width: 0;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	main h2 {
		font-size: 21px;
		margin: 0 0 10px;
	}

	.message {
		font-size: 14px;
		margin: 0 0 16px;
		min-height: 20px;
	}

	/* Square 5 x 5 board */
	.board {
		width: min(100%, 500px);
		aspect-ratio: 1 / 1;
		display: grid;
		grid-template-columns: repeat(5, minmax(0, 1fr));
		grid-template-rows: repeat(5, minmax(0, 1fr));
		gap: 6px;
		padding: 10px;
		background: #572052;
		border: 3px solid #e985dc;
		border-radius: 12px;
	}

	/* Every tile takes an equal share of the board */
	.tile {
		width: 100%;
		height: 100%;
		min-width: 0;
		min-height: 0;
		padding: 3px;
		border: 2px solid #c5a8a0;
		border-radius: 6px;
		background: #f5e5c9;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: default;
	}

	.tile:disabled {
		opacity: 1;
	}

	.tile.reachable {
		background: #ffe5a1;
		border: 3px solid #ffbd43;
		cursor: pointer;
		box-shadow: 0 0 8px rgba(255, 207, 89, 0.5);
	}

	.tile.reachable:hover {
		background: #ffd36d;
		transform: scale(0.96);
	}

	.tile.rat-tile {
		background: #efbce5;
		border-color: #e985dc;
	}

	.tile.key-tile {
		background: #ffe5a1;
	}

	.rat-sprite {
		width: 65%;
		height: 65%;
		object-fit: contain;
		pointer-events: none;
		transform: scale(1.7);
	}

	.key-sprite {
		width: 55%;
		height: 55%;
		object-fit: contain;
		pointer-events: none;
		transform: scale(1.7);
	}

	/* Dice sits beside the board */
	.dice-section {
		flex: 0 0 220px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		margin-top: 0;
		padding-bottom: 0;
	}

	.dice-section h2 {
		margin-bottom: 5px;
	}

	.dice-section p {
		font-size: 13px;
	}

	.dice {
		width: 100px;
		height: 100px;
		margin: 15px 0;
		filter: drop-shadow(0 6px 5px rgba(0, 0, 0, 0.2));
	}

	.dice.rolling {
		animation: diceRoll 0.7s ease-in-out;
	}

	@keyframes diceRoll {
		0% {
			transform: rotate(0deg) translateY(0);
		}
		25% {
			transform: rotate(90deg) translateY(-15px);
		}
		50% {
			transform: rotate(180deg) translateY(0);
		}
		75% {
			transform: rotate(270deg) translateY(-15px);
		}
		100% {
			transform: rotate(360deg) translateY(0);
		}
	}

	.roll-button {
		width: 220px;
		padding: 15px;
		border: 2px solid #e985dc;
		border-radius: 10px;
		background: #ffcf59;
		color: #3b0936;
		font-size: 16px;
		font-weight: bold;
		cursor: pointer;
	}

	.roll-button:hover:not(:disabled) {
		background: #ffe39a;
	}

	.roll-button:disabled {
		opacity: 0.65;
		cursor: not-allowed;
	}

	.success-message {
		color: #ffcf59;
		font-weight: bold;
		font-size: 16px;
	}

	/* Stack the dice below the board on smaller screens */
	@media (max-width: 650px) {
		.game-page {
			padding: 15px 12px;
		}

		.game-layout {
			flex-direction: column;
			gap: 20px;
		}

		.board-area {
			width: 100%;
			flex: none;
		}

		.board {
			gap: 4px;
			padding: 7px;
		}

		.dice-section {
			flex: none;
			margin-top: 10px;
			padding-bottom: 20px;
		}

		.info-bar {
			gap: 8px;
		}
	}
</style>
