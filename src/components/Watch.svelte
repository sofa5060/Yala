<script>
  export let time = 20;
  export let timerActive;
  export let seconds;
  export let minutes

</script>

<div class="watch">
  <h1>{minutes} : {seconds}</h1>
</div>

<style>
  .watch {
    max-width: 300px;
    margin: 10% auto 50px auto;
  }

  h1 {
    text-align: center;
    color: #fff;
    font-size: 80px;
  }
</style>
