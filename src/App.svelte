<script>
  import { onMount } from "svelte";

  let wordgrid = [];
  const boardsize = 5;

  onMount(() => {
    fetch("wordlist-eng.txt")
      .then((response) => response.text())
      .then((text) => {
        const words = text.split("\n");

        for (let i = 0; i < boardsize; i++) {
          wordgrid[i] = [];
          for (let j = 0; j < boardsize; j++) {
            let randomIndex = Math.floor(Math.random() * words.length);
            wordgrid[i][j] = words[randomIndex];
            words.splice(randomIndex, 1);
            console.log(words);
          }
        }
        console.log(wordgrid);
      });
  });
</script>

<main>
  <h1 class="grid">WebE Codenames</h1>
  {#each wordgrid as row}
    <div>
      {#each row as word}
        <button class="griditem">{word}</button>&nbsp;&nbsp;
      {/each}
    </div>
  {/each}
</main>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 10px;
  }

  .griditem {
    height: 100px;
    width: 150px;
    background-color: #f1f1f1;
    border: 1px solid black;
    text-align: center;
    font-size: 14px;
    margin: 4px 2px;
    cursor: pointer;
    transition: background-color 0.5s;
  }
</style>
