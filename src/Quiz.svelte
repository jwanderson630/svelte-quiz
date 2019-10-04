<script>
  export let quizName = "Quizzy Quiz";
  let result = "";
  let correctAnswer = "B";
  let answers = ["A", "B", "C", "D"];
  function pickAnswer(answer) {
    if (answer == correctAnswer) {
      return (result = "Correct!");
    } else {
      return (result = "Wrong!");
    }
  }
</script>

<style>
  .quizButtons {
    width: 90vw;
    max-width: 400px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minMax(50px, 1fr));
    grid-gap: 10px;
  }
  button {
    display: block;
  }
</style>

{#if result}
  <h2>{result}</h2>
{:else}
  <h2>Pick an answer!</h2>
{/if}
<div class="quizButtons">
  {#each answers as answer}
    <button on:click={() => pickAnswer(answer)}>{answer}</button>
  {/each}
</div>
