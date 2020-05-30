<script>
	import Tabs from "./components/Tabs.svelte"
	import Watch from "./components/Watch.svelte"
	import Navbar from "./components/Navbar.svelte"
	import Button from "./components/Button.svelte"
	let tabs = ['study','work','focus']
	let activeTab = 'study';
	let showTabs = false;
	let fullTime = 1500;
	$: time = fullTime
	let timerActive = false;
	let breakTime = 300;
	let mood = 'focus'

	$: intervalsArr = [];

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
	$:console.log(time)

</script>

{#if showTabs}
	<Tabs {tabs} on:changeTab={changeTab}/>
{/if}

<main>
	<Navbar />
	<Watch {timerActive} {time} {seconds} {minutes}/>
	<Button on:click={toggleActive} {timerActive} {time} {fullTime} {breakTime} {mood}/>
</main>

<style>
	main{
		background: rgb(233, 73, 73) !important;
	}
</style>