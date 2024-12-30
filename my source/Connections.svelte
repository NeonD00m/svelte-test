<script>
    import { send, receive } from './transition.js';
	import { writable } from 'svelte/store';

    const width = 100;
    const height = 50;

    export let words = [
        ['one', 'two', 'three', 'four'],
        ['apple', 'banana', 'orange', 'tomato'],
        ['the', 'earth', 'is', 'flat'],
        ['blue', 'red', 'peach', 'vanilla']
    ];
    let allWords = [];
    words.array.forEach(solution => {
        solution.array.forEach(word => {
            allWords.push(word);
        })
    });
    //randomize the all words positions
    let positions = words.;
    let selected = words.map((w, i) => writable(false));

    function selectWord(index) {
        let wasSelected = selected[index];


    }
</script>

<div class="container">
    {#each words as word, i (i)}
        <button
            class="word-object"
            on:click={()=>{selectWord(i)}}
			in:receive={{key: word}}
			out:send={{key: word}}
        >
            {word.toUpperCase()}
        </button>
    {/each}
</div>