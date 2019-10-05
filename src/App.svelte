<script>
  import Quiz from "./Quiz.svelte";
</script>

<style>
  :global(*) {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    box-sizing: border-box;
  }
  main {
    width: 90vw;
    max-width: 600px;
    margin: 50px auto;
    box-sizing: border-box;
    box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.2),
      2px 2px 11px 4px rgba(0, 0, 0, 0.05);
    border-radius: 1rem;
    padding: 3rem;
    background: #fff;
  }
  h1 {
    margin-top: 4rem;
    text-align: center;
  }
</style>

<h1>Quick Quizzy Quiz!</h1>
<main>
  <Quiz />
</main>
