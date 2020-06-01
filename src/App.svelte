<script>
	import Tabs from "./components/Tabs.svelte"
	import Watch from "./components/Watch.svelte"
	import Navbar from "./components/Navbar.svelte"
	import Button from "./components/Button.svelte"
	import Rounds from "./components/Rounds.svelte"
	let tabs = ['study','work','focus']
	let activeTab = 'focus';
	let showTabs = true;
	let fullTime = 1500;
	$: time = mood === 'break' ? breakTime : fullTime 
	let timerActive = false;
	let breakTime = 300;
	let mood = 'focus'
	$: intervalsArr = [];
	let rounds = 0;
	let goal = 12;

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
		if (mood === 'focus' && rounds % 4 === 3) {
			time = fullTime;
			mood = 'longBreak'
			rounds++
			toggleTimer()
		}else if(mood === 'focus'){
			time = breakTime;
			mood ='break'
			rounds++
			toggleTimer()
		}else{
			time = fullTime;
			mood = 'focus'
			toggleTimer()
		}
	}

	const addMinute = () => {
		intervalsArr.forEach(clearInterval)
		timerActive = false
		if (mood === 'break') {
			breakTime += 60
		}else{
			fullTime += 60
		}
	}

	const removeMinute = () => {
		intervalsArr.forEach(clearInterval)
		timerActive = false
		if (mood === 'break') {
			if(breakTime > 60){
				breakTime -= 60
			}
		}else{
			if(fullTime > 60){
			fullTime -= 60
			}
		}
	}

  $: minutes = Math.floor(time / 60) || "00";
	$: seconds = Math.floor(time % 60) || "00";
	$: time === 0 && changeMood();

</script>

{#if showTabs}
	<Tabs {tabs} on:changeTab={changeTab}/>
{/if}

<main class:focus={activeTab === "focus"} class:study={activeTab === "study"} class:work={activeTab === "work"} class:break={mood === "break" || mood === "longBreak"}>
	<Navbar {activeTab} {mood}/>
	<Watch {timerActive} {time} {seconds} {minutes} on:addMinute={addMinute} on:removeMinute={removeMinute}/>
	<Button on:click={toggleActive} {timerActive} {time} {fullTime} {breakTime} {mood}/>
	<Rounds {rounds} />
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