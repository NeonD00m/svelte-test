<script>
	let count = 0;
	$: doubled = count * 2;

	function increment() {
		count += 1;
	}

	import PackageInfo from './PackageInfo.svelte';

	const pkg = {
		name: 'svelte',
		speed: 'blazing',
		version: 4,
		website: 'https://svelte.dev'
	};
</script>

<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>{count} doubled is {doubled}</p>

<PackageInfo
	name={pkg.name}
	speed={pkg.speed}
	website={pkg.website}
/>