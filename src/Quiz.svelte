<script>
  import { onMount } from "svelte";
  import Buttons from "./Buttons.svelte";
  let result = "";
  let gameComplete = false;
  let score = 0;
  let displayResult = false;
  let quiz = undefined;
  let currentQuestionIndex = 0;
  $: currentQuestion = quiz ? quiz[currentQuestionIndex] : undefined;
  $: correctAnswer = quiz ? currentQuestion.correct_answer : undefined;
  $: answers = quiz
    ? randomizeAnswers([
        currentQuestion.correct_answer,
        ...currentQuestion.incorrect_answers
      ])
    : undefined;

  function randomizeAnswers(options) {
    const sortedAnswers = [];
    for (let i = 0; i < options.length; i++) {
      const randomNum = ~~(100 - 100 * Math.random);
      if (randomNum > 50) {
        sortedAnswers.push(options[i]);
      } else {
        sortedAnswers.unshift(options[i]);
      }
    }
    return sortedAnswers;
  }

  onMount(getQuiz);

  async function getQuiz() {
    const result = await fetch("https://opentdb.com/api.php?amount=3")
      .then(data => data.json())
      .then(({ results }) => results)
      .then(questions =>
        questions.map(({ question, correct_answer, incorrect_answers }) => {
          return {
            question,
            correct_answer,
            incorrect_answers
          };
        })
      );
    quiz = result;
  }

  function checkAnswer({ detail: answer }) {
    displayResult = true;
    if (answer == correctAnswer) {
      score++;
      result = "Correct!";
    } else {
      result = "Wrong!";
    }
    setTimeout(() => {
      displayResult = false;
      nextQuestion();
    }, 1000);
  }

  function nextQuestion() {
    if (currentQuestionIndex < quiz.length - 1) {
      currentQuestionIndex++;
    } else {
      gameComplete = true;
    }
  }

  async function resetGame() {
    score = 0;
    gameComplete = false;
    quiz = undefined;
    await getQuiz();
    currentQuestionIndex = 0;
  }
</script>

<style>
  .result {
    text-align: center;
    font-size: 2.5rem;
    font-weight: bold;
    margin: 1.5rem 0;
  }
</style>

{#if !gameComplete}
  {#if currentQuestion}
    <h2>
      {@html currentQuestion.question}
    </h2>
    {#if displayResult}
      <div class="result">{result}</div>
    {:else}
      <Buttons on:answer={checkAnswer} {answers} />
    {/if}
  {:else}
    <h2 style="text-align: center;">loading...</h2>
  {/if}
{:else}
  <h2>Your score was {score} out of {quiz.length}!</h2>
  <button on:click={resetGame}>Play again?</button>
{/if}
