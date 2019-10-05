<script>
  import { createEventDispatcher } from "svelte";
  export let disable = false;

  const dispatch = createEventDispatcher();
  export let answers = ["A", "B", "C", "D"];
  function submitAnswer(answer) {
    dispatch("answer", answer);
  }
</script>

<style>
  .quizButtons {
    width: 90vw;
    max-width: 100%;
    display: grid;
    grid-gap: 10px;
  }
  button {
    display: block;
    margin: 0;
    user-select: none;
    text-align: left;
  }
</style>

<div class="quizButtons">
  {#each answers as answer}
    <button on:click={() => submitAnswer(answer)}>
      {@html answer}
    </button>
  {/each}
</div>
