<script setup>
import { ref } from "vue"

const aboutInfo = ref([
	{ label: "姓名", value: "陳心妍" },
	{ label: "Email", value: "chenyan910627@gmail.com", link: "mailto:cindy20020627@gmail.com" },
	{ label: "手機", value: "0974-009-350" },
	{ label: "學歷", value: "佛光大學 傳播學系" },
])

const skills = ref([
	{ title: "前端技能", items: ["HTML", "CSS", "JavaScript", "Vue.js", "Tailwind CSS"] },
	{ title: "版本控制", items: ["Git", "GitHub"] },
	{ title: "後端接觸", items: ["Node.js", "Express", "Prisma", "MySQL", "RESTful API"] },
])

const projects = ref([
	{
		name: "my-journal-app",
		desc: "日期 + 當日 memo 功能",
		url: "https://github.com/CHENPODO/my-journal-app",
	},
	{
		name: "PikaBlog_fronted",
		desc: "與友人協作開發部落格前端",
		url: "https://github.com/PikaBlog",
	},
	{
		name: "Vue__practice-",
		desc: "Vue 練習作品集",
		url: "https://github.com/CHENPODO/Vue__practice-",
	},
	{
		name: "Python_practise",
		desc: "日常 Python 練習",
		url: "https://github.com/CHENPODO/Python_practise",
	},
])
</script>

<template>
	<!-- 基本資料卡片 -->
	<section class="info-card-section">
		<div class="info-card about-card">
			<div class="left-col">
				<img class="myself" alt="陳心妍 大頭貼" />
			</div>
			<div class="right-col">
				<h2>基本資料</h2>
				<ul>
					<li v-for="(item, idx) in aboutInfo" :key="idx">
						<span class="label">{{ item.label }}</span>
						<span class="value" v-if="item.link">
							<a :href="item.link">{{ item.value }}</a>
						</span>
						<span class="value" v-else>{{ item.value }}</span>
					</li>
				</ul>
				<!-- 技能卡片 -->
				<div class="skills-section">
					<div class="bottom-line"></div>
					<h2>技能</h2>
					<div v-for="(group, idx) in skills" :key="idx" class="skill-block">
						<h3>{{ group.title }}</h3>
						<ul class="skill-list">
							<li v-for="(skill, i) in group.items" :key="i">{{ skill }}</li>
						</ul>
					</div>
					<!-- 專案卡片 -->
					<div class="mt-section"></div>
					<div class="bottom-line"></div>
					<h2>GitHub 專案</h2>
					<div v-for="(project, idx) in projects" :key="idx" class="project-block">
						<h3 class="project-title">{{ project.name }}</h3>
						<p class="project-desc">{{ project.desc }}</p>
						<a :href="project.url" target="_blank" class="project-link">查看 GitHub</a>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<style scoped>
/* 整體卡片區 */
.info-card-section {
	background: #f9fafb;
	padding: 60px 20px;
	display: flex;
	justify-content: center;
}

.info-card {
	background: white;
	border-radius: 16px;
	max-width: 800px;
	width: 100%;
	padding: 40px 50px;
	box-shadow: 0 12px 24px rgba(0, 0, 0, 0.08);
	color: #3b3a57;
}

/* About 區左右欄 */
.about-card {
	display: flex;
	gap: 40px;
	align-items: flex-start;
}

.left-col {
	width: 200px; /* 固定左邊欄寬度 */
}

.myself {
	cursor: pointer;
	background-image: url(../assets/pic/IMG_4616.JPG);
	background-size: cover;
	background-position: center;
	background-repeat: no-repeat;
	width: 120px;
	height: 120px;
	object-fit: cover;
	border-radius: 50%;
	border: 4px solid #deddf7;
	box-shadow: 0 10px 20px rgba(132, 117, 176, 0.15);
	transition: transform 0.3s ease;
}

.myself:hover {
	transform: scale(1.05);
}
.myself img {
	width: 100%;
}
.right-col {
	flex: 1;
}

/* 右側資料 */
.right-col h2 {
	margin-bottom: 24px;
	font-weight: 700;
	font-size: 1.8rem;
	color: #9c5ce7;
	letter-spacing: 0.06em;
}

.right-col ul {
	list-style: none;
	padding: 0;
	margin: 0;
}

.right-col li {
	display: flex;
	padding: 14px 0;
	border-bottom: 1px solid #ececf7;
	font-size: 1.1rem;
	align-items: center;
}

.right-col li:last-child {
	border-bottom: none;
}
.skills-section {
	position: relative;
	margin-top: 40px;
}
.bottom-line::before {
	content: "";
	position: absolute;
	border: 0;
	width: 100%;
	height: 1px;
	border-bottom: #3b3a57 1px solid;
}
.mt-section {
	margin-top: 40px;
}
.label {
	width: 100px;
	font-weight: 600;
	color: #8e8bcf;
	letter-spacing: 0.05em;
}

.value {
	flex: 1;
	color: #4a4a68;
}

a {
	color: #6c5ce7;
	text-decoration: none;
	font-weight: 600;
	transition: color 0.2s ease;
}

a:hover {
	color: #4b3ca7;
	text-decoration: underline;
}

/* 技能區 */
.info-card h2 {
	font-size: 1.8rem;
	color: #6c5ce7;
	text-align: center;
	margin-bottom: 30px;
	font-weight: 700;
}

.skill-block {
	margin-bottom: 30px;
}

.skill-block h3 {
	font-weight: 600;
	font-size: 1.2rem;
	margin-bottom: 14px;
	color: #3b3a57;
}

.skill-list {
	display: flex;
	flex-wrap: wrap;
	gap: 12px;
	justify-content: center;
}

.skill-list li {
	background-color: #e9e7fd;
	color: #5f5ea7;
	padding: 6px 14px;
	border-radius: 12px;
	font-weight: 500;
	font-size: 1rem;
}

.project-block {
	padding: 20px 20px 20px 24px;
	border-left: 5px solid #6c5ce7;
	background: #f3f2fd;
	border-radius: 12px;
	margin-bottom: 20px;
	transition: box-shadow 0.3s ease;
}

.project-block:hover {
	box-shadow: 0 6px 16px rgba(108, 92, 231, 0.3);
}

.project-title {
	font-weight: 700;
	font-size: 1.2rem;
	color: #5e4b8b;
	margin-bottom: 6px;
}

.project-desc {
	font-size: 1rem;
	color: #6a6a8a;
	margin-bottom: 8px;
}

.project-link {
	font-weight: 600;
	color: #6c5ce7;
	text-decoration: underline;
	font-size: 1rem;
}

.project-link:hover {
	color: #4b3ca7;
}
</style>
