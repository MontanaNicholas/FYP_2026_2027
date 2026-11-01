
<script>
	let roll = $state(0);
	let isRolling = $state(false);

	function rollDice() {
		if (isRolling) return;

		roll = Math.floor(Math.random() * 6) + 1;
		isRolling = true;

		setTimeout(() => {
			isRolling = false;
		}, 700);
	}
</script>

<div class="body-container">

	<header>
		<h1>OH, RATS!</h1>
		<p>Rat 1's turn</p>
	</header>

	<main>
		{#if roll === 0}

			<h2>CLICK TO ROLL</h2>

		{:else}

			<p class="result-label">YOUR ROLL</p>

			<div class="result">
				{roll}
			</div>

			<h2>Move up to {roll} tiles</h2>

		{/if}

		<!-- Custom cream dice -->
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

			<!-- One, three and five dots -->
			{#if roll === 0 || roll === 1 || roll === 3 || roll === 5}
				<circle cx="60" cy="60" r="7" fill="#49372C" />
			{/if}

			<!-- Two, three, four, five and six dots -->
			{#if roll >= 2}
				<circle cx="36" cy="36" r="7" fill="#49372C" />
				<circle cx="84" cy="84" r="7" fill="#49372C" />
			{/if}

			<!-- Four, five and six dots -->
			{#if roll === 4 || roll === 5 || roll === 6}
				<circle cx="84" cy="36" r="7" fill="#49372C" />
				<circle cx="36" cy="84" r="7" fill="#49372C" />
			{/if}

			<!-- Six dots -->
			{#if roll === 6}
				<circle cx="36" cy="60" r="7" fill="#49372C" />
				<circle cx="84" cy="60" r="7" fill="#49372C" />
			{/if}

		</svg>

		{#if roll === 0}
			<button onclick={rollDice} disabled={isRolling}>
				ROLL DICE
			</button>
		{:else}
			<button onclick={rollDice} disabled={isRolling}>
				ROLL AGAIN
			</button>
		{/if}

	</main>

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
		min-height: 100vh;
		padding: 25px 20px;
		box-sizing: border-box;
	}

	header {
		width: 100%;
		max-width: 500px;
	}

	h1 {
		font-size: 28px;
		margin-bottom: 5px;
	}

	header p {
		color: #666;
		margin-top: 0;
	}

	main {
		width: 100%;
		max-width: 500px;
		min-height: 450px;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		text-align: center;
	}

	main h2 {
		font-size: 23px;
		font-weight: normal;
	}

	.result-label {
		color: #666;
		font-size: 20px;
		margin-bottom: 0;
	}

	.result {
		font-size: 100px;
		font-weight: bold;
		margin: 15px 0;
	}

	.dice {
		width: 130px;
		height: 130px;
		margin: 25px 0;
		filter: drop-shadow(0 6px 5px rgba(0, 0, 0, 0.12));
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

	button {
		width: 100%;
		max-width: 280px;
		padding: 18px;
		font-size: 18px;
		font-weight: bold;
		cursor: pointer;
		border: none;
		border-radius: 10px;
		background: #333;
		color: white;
		transition: background 0.2s;
	}

	button:hover {
		background: #555;
	}

	button:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}

	@media (min-width: 700px) {
		main {
			min-height: 600px;
		}
	}
</style>
