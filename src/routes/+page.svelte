<script lang="ts">
	import { onMount } from "svelte";
    import { compliments } from '$lib/compliments'

    let d = new Date();
    const timestamp = Date.now();
    $: hour = d.getHours();
    $: minute = d.getMinutes();
    $: seconds = d.getSeconds();
    $: displayHour = hour.toString();
    $: displayMinute = minute.toString().padStart(2, '0');
    $: displaySeconds = seconds.toString().padStart(2, '0');

    $: if(hour > 12) {
        hour = hour - 12
    }

    $: bgUrl = '';

    let index = Math.floor(Math.random() * compliments.length)

    const newCompliment = () => index = Math.floor(Math.random() * compliments.length)

    // const fetchBackground = async () => {
    //     const res = await fetch('https://picsum.photos/1920/1080')
    //     bgUrl = res.url
    //     console.log(bgUrl)
    // }

	onMount(() => {
		const interval = setInterval(() => {
			d = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<div class="flex h-screen bg-cover bg-[url('https://picsum.photos/1920/1080')]">
    <div class="m-auto text-center text-white">
        <h1 class="text-6xl pb-5" style="text-shadow: 3px 2px 0 #000">It is now:</h1>
        <h1 class="text-8xl pb-5" style="text-shadow: 3px 2px 0 #000">{displayHour}:{displayMinute}:{displaySeconds}</h1>
        <h1 class="text-6xl pb-8" style="text-shadow: 3px 2px 0 #000">{compliments[index]}</h1>
        <button class="btn" on:click={newCompliment}>New Compliment</button>
        <!-- <button class="btn" on:click={fetchBackground}>Background</button> -->
    </div>
</div>