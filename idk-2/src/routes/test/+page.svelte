<script>
	let count = 0;
	$: doubled = count * 2;

	function increment() {
		count += 1;
	}

	// import PackageInfo from './PackageInfo.svelte';

	const pkg = {
		name: 'svelte',
		speed: 'blazing',
		version: 4,
		website: 'https://svelte.dev'
	};

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
	let selected = colors[0];

	// import { getRandomNumber } from './utils.js';

	// let promise = getRandomNumber();

	// function handleClick() {
	// 	promise = getRandomNumber();
	// }

	let mailCheckBox = false;
</script>

<style>
	h1 {
		transition: color 0.2s;
	}

	/* .clr-div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	} */

	.clr-button {
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
	}

	.clr-button[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0,0,0,0.2);
	}
</style>

<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>{count} doubled is {doubled}</p>

{#if count > 7}
	<p>{count} is greater than 7</p>
{:else if count < 3}
	<p>{count} is less than 3</p>
{:else}
	<p>{count} is between 3 and 7</p>
{/if}

<!-- <PackageInfo
	name={pkg.name}
	speed={pkg.speed}
	website={pkg.website}
/> -->

<h1 style="color: {selected}">Pick a colour</h1>

<div id="clr-div">
	{#each colors as color, i (i)}
		<button
			class="clr-button"
			aria-current={selected === color}
			aria-label={color}
			style="background: {color}"
			on:click={() => selected = color}
		>{i + 1}</button>
	{/each}
</div>

<!-- <button on:click={handleClick}>
	generate random number
</button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await} -->

<label>
	<input type="checkbox" checked={mailCheckBox} />
	Yes! Send me regular email spam
</label>

{#if mailCheckBox}
	<p>
		Thank you. We will bombard your inbox and sell
		your personal details.
	</p>
{:else}
	<p>
		You must opt in to continue. If you're not
		paying, you're the product.
	</p>
{/if}