<script>
import Slide 	   from './Slide.svelte'
import SlideButton from './SlideButton.svelte'
import Dot   	   from './Dot.svelte'

	let slides = ["1", "2", "3", "4"]; // Массив наших слайдов 
	let active = 1; 			       // Указывает какой номер слайда будет отображаться первым

	function increment() {
		const newActive = (active + 1) % slides.length;
        updateActive(newActive);
	}
	function decrement() {
		const newActive = (active - 1 + slides.length) % slides.length;
        updateActive(newActive);
	}
	function updateActive(newActive) {
		active = newActive;
    }
</script>

<main>
	<div class="flex items-center justify-center mt-40 mb-10 gap-4">
		<SlideButton on:click={decrement} content="-"/>
		<Slide slides={slides} active={active} />
		<SlideButton on:click={increment} content="+"/>
	</div>
	<Dot dots={slides} active={active}/> 
</main>