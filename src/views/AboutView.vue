<script setup>
import IconPic from "@/assets/pic/icon.png"
</script>
<template>
	<section class="myself">
		<div class="myself-text">
			<h1 class="text-4xl font-bold text-gray-800">
				CHEN
				<span class="highlight">Podo</span>
			</h1>
			<p class="highlight font-bold text-4xl">這裡有一些我的小東西:P</p>
		</div>
		<div class="pic-image">
			<img :src="IconPic" alt="PODO.PIC" />
		</div>
	</section>
</template>
<style>
/* Reset default margins */
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

/* Navigation Bar */
.navbar {
	display: flex;
	justify-content: space-between;
	padding: 20px;
	background: transparent;
}

.myself {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 80px;
	background: #ffffff;
	height: 90vh;
}

.myself-text {
	max-width: 50%;
}

.myself-text h1 {
	font-size: 4rem;
	color: #333;
}

.myself-text .highlight {
	color: #8475b0; /* Teal color */
}

.myself-text p {
	font-size: 1.2rem;
	color: #666;
	margin-top: 20px;
}

/* pic Image */
.pic-image img {
	max-width: 300px;
	border-radius: 30px;
	box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
	transition: transform 1.5s ease; /* 加上過渡動畫 */
}
.pic-image img:hover {
	transform: scale(1.5) rotate(360deg) scale(0.5);
}
</style>
