<script>
export let name;
export let slides;

document.addEventListener('DOMContentLoaded', () => {
    var blocks = document.querySelectorAll(".block"); // Картинки (слайды)
	var dots   = document.querySelectorAll(".dot");   // Кнопки навигации
    var currentIndex   = 0; 						  // Начальный индекс активного элемента
	const contentWidth = document.querySelector(".content").offsetWidth;
    
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
			};
		};

		// Позеционируем слайды относительно активного
		for (let i = 0; i < blocks.length; i++) {
			const offsetFromActive = (i - currentIndex) * 100;
			const x = centerX + offsetFromActive;
			blocks[i].style.transform = `translate(${x}px, 0px)`;
			i != currentIndex && (dots[i].style.backgroundColor = "#ccc");
		};
	}

	start();
	let increment = document.getElementById("increment");
    increment.addEventListener('click', () => {
        var newIndex = (currentIndex + 1) % blocks.length;
        updateActive(newIndex);
		start();
    });

	let decrement = document.getElementById("decrement");
    decrement.addEventListener('click', () => {
        var newIndex = (currentIndex - 1 + blocks.length) % blocks.length;
        updateActive(newIndex);
		start();
    });

	// Функция для обновления активного элемента
    function updateActive(newIndex) {
        blocks[currentIndex].classList.remove('active');
        blocks[newIndex].classList.add('active');
        currentIndex = newIndex;
    }
});

</script>

<main>
	<div class="slider row">
		<button id="decrement">-</button>
		<div class="content row">
			<div class="block">1</div>
			<div class="block active">2</div>
			<div class="block">3</div>
			<div class="block">4</div>
		</div>
		<button id="increment">+</button>
	</div>
	<div class="dots">
		<p class="dot"></p>
		<p class="dot"></p>
		<p class="dot"></p>
		<p class="dot"></p>
	</div>
</main>

<style>
	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}
	.slider {
		align-items: center;
		margin: 10vh auto;
		justify-content: center;
	}
	.slider > button {
		background: #a591915d;
		color: #FFF;
		margin: 10px;
		height: 40px;
	}
	.slider > button:hover {
		opacity: 0.7;
		cursor: pointer;
	}
	#decrement, #increment {
		z-index: 1; /* Что бы кнопки всегда прошелкивались поставим z-index кнопок > картинок слайдера */
	}
	.content > div { 
		background: #c11818; /* Используется заливка, но с картинками было бы сложнее они имеют свойство сжиматься, иногда это ломает верстку */
		border-radius: 20px;
		height: 200px; /* Фиксированная высота */
		transition: transform 0.4s ease;
		width: 40vw;  /* Адаптивная ширина, 40% от экрана */
	}
	.content > div:not(.active) {
		background: #c1181823;
		position: fixed;
		z-index: -1;
	}
	.dots {
		display: flex;
		justify-content: center;
		margin-top: 20px;
		gap: 10px;
	}
	.dot {
		background-color: #ccc;
		border-radius: 50%;
		transition: background-color 0.3s;
		height: 12px;
		width: 12px;
	}
</style>