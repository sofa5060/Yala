<script>
	import Tabs from "./components/Tabs.svelte"
	import Watch from "./components/Watch.svelte"
	import Navbar from "./components/Navbar.svelte"
	import Button from "./components/Button.svelte"
	let tabs = ['study','work','focus']
	let activeTab = 'focus';
	let showTabs = true;
	let fullTime = 1500;
	$: time = fullTime
	let timerActive = false;
	let breakTime = 300;
	let mood = 'focus'
	$: intervalsArr = [];

	const changeTab = (e) => {
		activeTab = e.detail
		showTabs = false
	}

	const toggleActive = () => {
		timerActive = !timerActive
		toggleTimer()
	}

	const toggleTimer = () => {
		if (timerActive && time > 0){
			let i = setInterval(() => {
				time--;
			}, 1000);
			intervalsArr.push(i)
		}else{
			intervalsArr.forEach(clearInterval)
		}
	}

	const changeMood = () => {
		intervalsArr.forEach(clearInterval)
		if (mood === 'focus') {
			time = breakTime;
			toggleTimer()
			mood ='break'
		}else{
			time = fullTime;
			toggleTimer()
			mood = 'focus'
		}
	}

  $: minutes = Math.floor(time / 60) || "00";
	$: seconds = Math.floor(time % 60) || "00";
	$: time === 0 && changeMood();

</script>

{#if showTabs}
	<Tabs {tabs} on:changeTab={changeTab}/>
{/if}

<main class:focus={activeTab === "focus"} class:study={activeTab === "study"} class:work={activeTab === "work"} class:break={mood === "break"}>
	<Navbar {activeTab} {mood}/>
	<Watch {timerActive} {time} {seconds} {minutes}/>
	<Button on:click={toggleActive} {timerActive} {time} {fullTime} {breakTime} {mood}/>
</main>

<style>
	main{
		min-width: 100vw;
		min-height: 100vh;
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