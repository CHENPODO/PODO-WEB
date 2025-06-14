<script setup>
import { ref } from "vue"
import { RouterLink, RouterView } from "vue-router"

const isMenuOpen = ref(false)

function toggleMenu() {
	isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
	<div>
		<header>
			<div class="bg-gray-50 wrapper border-gray-200 border-2">
				<nav>
					<div class="nav-left">
						<h1><RouterLink to="/">PODO</RouterLink></h1>
					</div>

					<!-- 漢堡圖示：一直顯示在電腦版 -->
					<div class="hamburger" @click="toggleMenu">
						<span></span>
						<span></span>
						<span></span>
					</div>

					<!-- 導覽選單：一開始隱藏，點漢堡才顯示 -->
					<div class="nav-right" :class="{ open: isMenuOpen }">
						<RouterLink to="/detail">履歷表</RouterLink>
						<RouterLink to="/:pathMatch(.*)*">Not Found</RouterLink>
						<RouterLink to="/post">文章</RouterLink>
						<a href="https://left-and-right-accessory.up.railway.app/" target="_blank">left-and-right 專案</a>
					</div>
				</nav>
			</div>
		</header>

		<RouterView />
	</div>
</template>

<style scoped>
.wrapper {
	max-width: 1200px;
	margin: 0 auto;
	padding: 0 40px;
}

nav {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 20px 0;
	position: relative;
}

/* 左邊 Logo */
.nav-left h1 {
	font-size: 2rem;
	font-weight: 700;
	color: #333;
}

/* 導覽列：預設隱藏，點擊後橫向展開 */
.nav-right {
	display: none;
	flex-direction: row;
	gap: 20px;
	position: absolute;
	top: 100%;
	right: 0;
	background-color: whitesmoke;
	box-shadow: 1px 1px 1px 1px;
	padding: 10px 20px;
	border-radius: 5px;
	z-index: 10;
}

.nav-right.open {
	display: flex;
	flex-direction: column;
}

.nav-right a {
	text-decoration: none;
	color: whitesmoke;
	background-color: rgb(171, 150, 180);
	font-weight: 500;
	padding: 5px 10px;
	border-radius: 3px;
	transition: ease-in-out 0.3s;
}

.nav-right a:hover {
	transform: translateY(-8px);
	background-color: rgb(147, 130, 154);
}

.hamburger {
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	width: 25px;
	height: 18px;
	cursor: pointer;
}

.hamburger span {
	display: block;
	height: 3px;
	width: 100%;
	background-color: #333;
	border-radius: 2px;
}
</style>
