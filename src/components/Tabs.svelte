<script>
  import {createEventDispatcher} from "svelte"
  import {scale , fade , slide } from "svelte/transition"
  let dispatch = createEventDispatcher()
  export let tabs;

  const handleClick = (tab) => {
    dispatch('changeTab',tab)
  }
</script>

<div class="background" transition:fade|local={{duration:500}}>
  <div class="tabs" transition:scale|local={{duration:500}}>
    <h3>What are you going to do ?</h3>
    <ul>
      {#each tabs as tab}
        <li on:click={() => handleClick(tab)}>{tab}</li>
        <hr />
      {/each}
    </ul>
  </div>
</div>

<style>
  .background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
    z-index: 10;
  }

  .tabs {
    background: #000;
    max-width: 300px;
    margin: 10% auto;
    padding: 70px 20px;
    text-align: center;
    border-radius: 25px;
    color: #fff;
  }

  ul {
    margin: 20px 0 0 0;
    padding: 0;
  }

  li {
    list-style: none;
    cursor: pointer;
    font-size: 22px;
    margin: 10px 0;
  }
</style>
