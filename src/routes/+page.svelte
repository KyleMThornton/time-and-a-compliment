<script lang="ts">
	import { onMount } from "svelte";

    let d = new Date();
    $: hour = d.getHours();
    $: minute = d.getMinutes();
    $: seconds = d.getSeconds();
    $: displayHour = hour.toString().padStart(2, '0');
    $: displayMinute = minute.toString().padStart(2, '0');
    $: displaySeconds = seconds.toString().padStart(2, '0');

    $: if(hour > 12) {
        hour = hour - 12
    }

    let compliment = ['test', 'test2', 'test3', 'test4', 'test5']
    let index = 0

    const newCompliment = () => index === 4 ? index = 0 : index++

	onMount(() => {
		const interval = setInterval(() => {
			d = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<div class="flex h-screen random">
    <div class="m-auto text-center">
        <h1 class="text-6xl pb-5">It is now:</h1>
        <h1 class="text-8xl pb-5">{displayHour}:{displayMinute}:{displaySeconds}</h1>
        <h1 class="text-6xl pb-5">{compliment[index]}</h1>
        <button class="btn" on:click={newCompliment}>New</button>
    </div>
</div>