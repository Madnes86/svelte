<script>
import { onMount } from 'svelte';
export let slides;

let blocks;
let dots;
let currentIndex = 0;

onMount(() => {
    blocks = document.querySelectorAll(".slide"); // Картинки (слайды)
    dots = document.querySelectorAll(".dot");     // Кнопки навигации
    const content = document.querySelector(".flex.justify-between"); // main slide
    const contentWidth = content.offsetWidth;

    // Находим начальный активный элемент
    function start() {
        const blockWidth = blocks[0].offsetWidth; // Предполагаем одинаковую ширину
        let centerX = (contentWidth / 2) - (blockWidth / 2);

        // Сначала найдем активный слайд
        for (let i = 0; i < blocks.length; i++) {
            if (blocks[i].classList.contains('active')) {
                currentIndex = i;
                dots[currentIndex].style.backgroundColor = "#333";
                break;
            }
        }

        // Позеционируем слайды относительно активного
        for (let i = 0; i < blocks.length; i++) {
            const offsetFromActive = (i - currentIndex) * 100;
            const x = centerX + offsetFromActive;
            blocks[i].style.transform = `translate(${x}px, 0px)`;
            if (i !== currentIndex) {
                dots[i].style.backgroundColor = "#ccc";
            }
        }
    }

    function updateActive(newIndex) {
        blocks[currentIndex].classList.remove('active');
        blocks[newIndex].classList.add('active');
        currentIndex = newIndex;
    }

    const increment = document.getElementById("increment");
    increment.addEventListener('click', () => {
        const newIndex = (currentIndex + 1) % blocks.length;
        updateActive(newIndex);
        start();
    });

    const decrement = document.getElementById("decrement");
    decrement.addEventListener('click', () => {
        const newIndex = (currentIndex - 1 + blocks.length) % blocks.length;
        updateActive(newIndex);
        start();
    });
	start();
});
</script>

<main>
	<div class="flex items-center justify-center mt-40 mb-10 gap-4">
		<button id="decrement" class="bg-gray-400 text-white h-10 px-4 rounded hover:opacity-70 z-10">-</button>
		<div class="flex justify-between w-full gap-4 relative overflow-hidden">
			{#each slides as slide, i}
				<div class="slide {i === currentIndex ? 'active' : ''}">{slide}</div>
			{/each}
		</div>
		<button id="increment" class="bg-gray-400 text-white h-10 px-4 rounded hover:opacity-70 z-10">+</button>
	</div>
	<div class="flex justify-center mt-5 gap-2">
		{#each slides as _, i}
			<p class="w-3 h-3 rounded-full bg-gray-300 transition-colors dot"></p>
		{/each}
	</div>
</main>