<script>
    export let dots
    export let active
</script>

<main class="flex justify-center mt-5 gap-2">
    {#each dots as _, i}
		<p class="w-3 h-3 rounded-full bg-gray-300 transition-colors dot {i === active ? 'bg-red-300' : ''}"></p>
	{/each}
</main>