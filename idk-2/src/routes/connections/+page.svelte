<script>
    import { send, receive } from './transition.js';
	import { writable } from 'svelte/store';

    const width = 100;
    const height = 50;

    const categories = ['numbers', 'fruit', 'sentence', 'colors'];
    const words = [
        ['one', 'two', 'three', 'four'],
        ['apple', 'banana', 'orange', 'tomato'],
        ['the', 'earth', 'is', 'flat'],
        ['blue', 'red', 'green', 'yellow']
    ];
    let allWords = [];
    words.array.forEach(solution => {
        solution.array.forEach(word => {
            allWords.push(word);
        })
    });
    //randomize the all words positions
    let positions = allWords.map((w, i) => writable({x: i % 4, y: Math.floor(i / 4)}));
    let selected = allWords.map((w, i) => writable(false));
    let selection = [];
    let solvedRows = 0;
    let rowToSolution = [];

    function findWordAt(row, column) {

    }

    function swapRow(index) {
        //swap the row of the word at index to the next available row (@ solvedRows)
        //find the word that was currently at that row
        let newRow = solvedRows;
        let index = findWordAt(newRow, index % 4);

    }

    function checkSolution() {
        if (selection.length < 4) {
            return;
        }

        let valid = 0;
        let category;
        words.forEach((solution, number) => {
            let thisSolutionWorks = 0;
            solution.forEach((word) => {
                thisSolutionWorks += (selection.includes(word) ? 1 : 0);
            })
            valid = Math.max(valid, thisSolutionWorks);
            if (thisSolutionWorks === 4) {
                category = categories[number];
            }
        });

        if (valid < 4) {
            alert(valid === 3 ? "one away" : "incorrect")
            return;
        }

        //its correct!
        //swap rows for all correct words in the category
        rowToSolution[solvedRows] = category;
        selection.forEach((word) => {
            swapRow(allWords.find(word));
        }));
        selection = [];
        solvedRows += 1;
    }

    function selectWord(index) {
        const word = allWords.at(index);
        let wasSelected = selected[index];
        selected[index].set(!wasSelected)
        if (!wasSelected) {
            selection.push(word)
        } else {
            selection[selection.find(word)] = null
        }

    }
</script>

<div class="container">
    {#each words as row, number (number)}
        <div class="row">
            <!-- do something with i to indicate which row it is in -->
            {#each row as word (allWords.find(number))}
                <button
                    class="word-object"
                    on:click={()=>{() => {selectWord(allWords.find(number))}}}
                    in:receive={{key: word}}
                    out:send={{key: word}}
                >
                    {word.toUpperCase()}
                </button>
            {/each}
            {#if solvedRows >= number}
                <div class="solution">
                    <p>
                        {categories}
                    </p>
                </div>
            {/if}
        </div>
    {/each}
    <div class="buttons">
        <button
            on:click{checkSolution}}
        >
            SUBMIT
        </button>
    </div>
</div>

<style>
    .row {
        background: none;
        
    }
</style>