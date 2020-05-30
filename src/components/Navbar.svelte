<script>
  export let activeTab;
  export let mood;
</script>

<nav class:focus={activeTab === "focus"} class:study={activeTab === "study"} class:work={activeTab === "work"} class:break={mood === "break"}>
  <h1>Yala!</h1>
  <h3>welcome to your dreams</h3>
</nav>

<style>
  nav{
    display: flex;
    max-width: 1300px;
    padding: 20px 50px;
    justify-content: space-between;
    align-self: center;
    color: #fff;
  }

  .focus{
		background: rgb(233, 73, 73);
	}
	.study{
		background: rgb(70, 153, 231);
	}
	.work{
		background: rgb(223, 171, 60);
  }
  .break{
		background: rgb(52, 214, 160) !important;
	}
</style>