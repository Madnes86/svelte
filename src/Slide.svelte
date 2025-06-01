<script>
    export let slides = [];
    export let active;
    export let blocks = [];
    export let contentDiv;

</script>

<main class="flex justify-between gap-4 relative overflow-hidden" bind:this={contentDiv}>
    {#each slides as slide, i}
        <div bind:this={blocks[i]} class="slide {i === active ? 'active' : ''}">{slide}</div>
    {/each}
</main>