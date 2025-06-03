<script>
import Slide 	   from './Slide.svelte'
import SlideButton from './SlideButton.svelte'
import Dot   	   from './Dot.svelte'
import Api 		   from './Api.svelte';

	let slides = ["1", "2"]; // Массив наших слайдов 
	let active = 1;   	 	 // Указывает какой номер - 1 слайда будет отображаться первым
	if (active >= slides.length) { // Проверка 
		active = slides.length - 1;
	}
	let MAX_SLIDES = 10;

	function getSlides() {
		fetch(`https://jsonplaceholder.typicode.com/posts/1`)
		.then((response) => response.json())
        .then((json) => {
            slides = json
        });
	}
	function addSlide() {
		var postNumber = slides.length;
		if (postNumber < MAX_SLIDES) {
			fetch(`https://jsonplaceholder.typicode.com/posts/${postNumber}`)
			.then((response) => response.json())
			.then((json) => {
				slides = [...slides, json];
			});
		} else {
			alert("Массив полон")
			console.log("Массив полон")
		}
	}
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
	<admin>
		<h1>Админ панель</h1>
		<button on:click={addSlide} class="rounded-[20px]">ADD</button>
	</admin>
</main>