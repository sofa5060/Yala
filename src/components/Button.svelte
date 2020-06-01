<script>
  import { tweened } from "svelte/motion";
  export let timerActive;
  export let time;
  export let fullTime;
  export let mood;
  export let breakTime;
  let currTime = time;
  $: passedTime = mood === 'focus' ||  mood === 'longBreak' ? fullTime - time : breakTime - time
  const length = tweened(0);
  $: currLength = mood === 'focus' ||  mood === 'longBreak' ? Math.floor((passedTime / fullTime) * 255) : Math.floor((passedTime / breakTime) * 255)
  $: length.set(currLength)
</script>

<div class="button" on:click>
  <svg>
    <circle r="40" cx="70" cy="0" style="stroke-dashoffset: {$length}px"></circle>
  </svg>
  {#if timerActive}
    <h3>stop</h3>
  {:else}
    <h3>Start</h3>
  {/if}
</div>

<style>
  .button {
    position: relative;
    margin: 0 auto;
    color: #fff;
    border-radius: 50%;
    text-align: center;
    cursor: pointer;
    width: 75px;
    height: 75px;
  }

  svg circle {
    stroke-dasharray: 255px;
    stroke-linecap: round;
    stroke-width: 2px;
    stroke: white;
    fill: none;
    width: 75px;
    height: 75px;
  }

  h3 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    position: relative;
  }

  svg {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
    overflow: visible;
    transform: rotateZ(-90deg);
  }
</style>
