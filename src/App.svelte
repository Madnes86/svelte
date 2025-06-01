<script>
import Slide 	   from './Slide.svelte'
import SlideButton from './SlideButton.svelte'
import Dot   	   from './Dot.svelte'

	let slides = ["1", "2", "3", "4"]; // Массив наших слайдов 
	let active = 1; 			  // Указывает какой номер слайда будет отображаться первым
	let blocks = []; 			  // Ссылка на DOM элемент массива slides
    let contentDiv;  			  // Ссыдка на DOM элемент слайдера
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
	function increment() {
		const newActive = (active + 1) % blocks.length;
        updateActive(newActive);
	}
	function decrement() {
		const newActive = (active - 1 + blocks.length) % blocks.length;
        updateActive(newActive);
	}
	function updateActive(newActive) {
		active = newActive;
    }
</script>

<main>
	<div class="flex items-center justify-center mt-40 mb-10 gap-4">
		<SlideButton on:click={decrement} content="-"/>
		<Slide slides={slides} active={active} bind:blocks bind:contentDiv />
		<SlideButton on:click={increment} content="+"/>
	</div>
	<Dot dots={slides} active={active}/> 
</main>