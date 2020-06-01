<script>
  import { createEventDispatcher } from "svelte";
  export let time = 20;
  export let timerActive;
  export let seconds;
  export let minutes;
  const dispatch = createEventDispatcher()

  const addMinute = () => {
    dispatch("addMinute")
  };

  const removeMinute = () => {
    dispatch("removeMinute")
  };
</script>

<div class="watch">
  <img src="./back.png" alt="arrow" on:click="{removeMinute}" />
  <h1>{minutes} : {seconds}</h1>
  <img src="./next.png" alt="arrow" on:click="{addMinute}" />
</div>

<style>
  .watch {
    max-width: 400px;
    margin: 8% auto 50px auto;
    display: flex;
    justify-content: space-between;
  }

  h1 {
    text-align: center;
    color: #fff;
    font-size: 80px;
    margin: 0 20px;
    justify-content: center;
  }

  img {
    max-width: 20px;
    cursor: pointer;
    height: 100%;
    max-height: 20px;
    display: block;
    align-self: center;
  }
</style>
