<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../shared/Card.svelte";
  export let poll;
  // reactive values
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentA = Math.floor((100 / totalVotes) * poll.votesA);
  $: percentB = Math.floor((100 / totalVotes) * poll.votesB);

  //handleVote
  const dispatch = createEventDispatcher();
  const handleVote = (option, id) => {
    dispatch("vote", { option, id });
  };
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <!-- emit custom events -->
    <div
      class="answer"
      on:click={() => {
        handleVote("a", poll.id);
      }}
    >
      <div class="percent percent-a" style="width: {percentA}%" />
      <!-- use dynamic values -->
      <span>{poll.answerA} ({poll.votesA} votes)</span>
    </div>
    <div
      class="answer"
      on:click={() => {
        handleVote("b", poll.id);
      }}
    >
      <div class="percent percent-b" style="width: {percentB}%" />
      <span>{poll.answerB} ({poll.votesB} votes)</span>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
    color: #555;
  }
  p {
    margin-top: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }

  .percent {
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }

  .percent-a {
    /* width: 25%; */
    border-left: 4px solid #d91b42;
    background: rgba(217, 27, 66, 0.2);
  }

  .percent-b {
    /* width: 75%; */
    border-left: 4px solid #45c496;
    background: rgba(69, 196, 150, 0.2);
  }
</style>
