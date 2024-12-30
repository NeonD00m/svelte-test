<script>
	let visible = false;

	function typewriter(node, { speed = 1 }) {
		const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

		if (!valid) {
			throw new Error(`This transition only works on elements with a single text node child`);
		}

		const text = node.textContent;
		const duration = text.length / (speed * 0.01);

		return {
			duration,
			tick: (t) => {
				const i = Math.trunc(text.length * t);
				node.textContent = text.slice(0, i);
			}
		};
	}
	let status = 'waiting...';
</script>

<p>status: {status}</p>

<label>
	<input type="checkbox" bind:checked={visible} />
	visible
</label>

{#if visible}
	<p transition:typewriter
    on:introstart={() => status = 'intro start'}
    on:outrostart={() => status = 'outro start'}
    on:introend={() => status = 'intro end'}
    on:outroend={() => status = 'outro end'}>
		The quick brown fox jumps over the lazy dog
	</p>
{/if}