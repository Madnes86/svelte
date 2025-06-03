<script>
    import { fade } from 'svelte/transition';

    export let slides;
    export let active;
    let blocks = [];              // Массив с DOM slide
    let contentDiv;               // Наш контейнер
    const SLIDE_INDENTATION = 100 // Наша константа отступа px от слайда

    $: if(slides.length && contentDiv) {
        const slideWidth = blocks[0].offsetWidth; // возможно стоит переименовать blocks в slideLink или slideDOM
        const contentWidth = contentDiv.offsetWidth;
        const centerX = (contentWidth / 2) - (slideWidth / 2);

        for (let i = 0; i < blocks.length; i++) {
            const offsetFromActive = (i - active) * SLIDE_INDENTATION;
            const x = centerX + offsetFromActive;
            blocks[i].style.transform = `translate(${x}px, 0px)`;
        }
    }
</script>

<!-- НАЙДЕН БАГ, ПОЧЕМУ ТО СЛАЙДЫ ПРИ СКРОЛЕ СМЕЩАЮТСЯ ВНИЗ ЦЕНТРИРУЯСЬ ПО ВЕРТИКАЛИ -->

<main class="flex justify-between gap-4 relative overflow-hidden" bind:this={contentDiv}>
  {#each slides as slide, i}
    <div
      bind:this={blocks[i]}
      class="slide {i === active ? 'active' : ''}"
    >
      {slide.title}
    </div>
  {/each}
</main>