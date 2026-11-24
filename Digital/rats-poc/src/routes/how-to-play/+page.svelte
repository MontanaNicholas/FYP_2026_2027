
<svelte:head>
	<title>How to Play | Oh, RATS!</title>
</svelte:head>

<div class="page">
    <main class="instruction-board">
        <a href="/rat-menu" class="back-button">BACK</a>

		<section class="instruction dice">
			<h2>ROLL THE DICE</h2>
			<p>Roll the dice to see how many tiles you can move.</p>
		</section>

		<section class="instruction movement">
			<h2>MOVE AROUND</h2>
			<p>Choose your route and move through the house, one tile at a time.</p>
		</section>

		<section class="instruction key">
			<h2>FIND THE KEY</h2>
			<p>The fridge is locked! Search the rooms to find the key.</p>
		</section>

		<section class="instruction trap">
			<h2>WATCH YOUR STEP</h2>
			<p>Hidden traps are scattered around the house. Be careful where you move!</p>
		</section>

		<section class="instruction cat">
			<h2>AVOID THE CAT</h2>
			<p>If the cat catches you, you'll need to defend yourself or escape.</p>
		</section>

		<section class="instruction fridge">
			<h2>REACH THE FRIDGE</h2>
			<p>Find the key, make it to the kitchen and unlock the fridge to win!</p>
		</section>
	</main>
</div>

<style>
	:global(body) {
		margin: 0;
		background: #3b0936;
		font-family: Arial, sans-serif;
	}

    .page {
    min-height: 100vh;
    padding: 4px 20px 20px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: center;
    }

    .back-button {
    position: absolute;
    top: 15px;
    left: 20px;
    z-index: 10;
    color: #ffcf59;
    text-decoration: none;
    font-weight: bold;
    }

	.instruction-board {
		position: relative;
		width: 100%;
		max-width: 680px;
		aspect-ratio: 2 / 3;
		background-image: url('/images/how-to-play.png');
		background-size: 100% 100%;
		background-repeat: no-repeat;
	}

	.instruction {
		position: absolute;
		width: 43%;
		height: 16%;
		box-sizing: border-box;
		padding: 12px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		color: #3b0936;
	}

	.instruction h2 {
		font-size: clamp(11px, 2vw, 17px);
		margin: 0 0 8px;
		font-weight: 900;
	}

    .instruction p {
    font-size: clamp(9px, 1.5vw, 13px);
    line-height: 1.4;
    margin: 0;
    width: 68%;
    text-align: center;
    }

	.dice {
		top: 34%;
		left: 3%;
	}

	.movement {
		top: 34%;
		left: 51%;
	}

	.key {
		top: 55.5%;
		left: 3%;
	}

	.trap {
		top: 55.5%;
		left: 51%;
	}

	.cat {
		top: 77%;
		left: 3%;
	}

	.fridge {
		top: 77%;
		left: 51%;
	}

	@media (max-width: 500px) {
		.page {
			padding: 10px;
		}

		.instruction {
			padding: 5px;
		}

		.instruction h2 {
			margin-bottom: 4px;
		}
	}
</style>
