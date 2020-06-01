<script>
  export let rounds;
  let groupRounds = rounds > 4 ?  rounds - Math.floor(rounds / 4) * 4 : rounds
</script>

<div class="background">
  <div class="rounds">
    <h3>ROUND</h3>
    <h5><span>{groupRounds}</span>/4</h5>
  </div>
  <hr />
  <div class="goal">
    <h3>GOAL</h3>
    <h5><span>{rounds}</span>/12</h5>
  </div>
</div>

<style>
  .background {
    background: #fff;
    display: flex;
    justify-content: space-evenly;
    position: fixed;
    width: 100vw;
    bottom: 0;
    z-index: 5;
    padding: 20px 0;
    text-align: center;
  }

  h3{
    font-size: 16px;
    font-weight: 600;
    margin: 0 0 20px 0;
  }

  h5{
    font-size: 14px;
  }

  span{
    font-size: 32px !important;
  }
</style>
