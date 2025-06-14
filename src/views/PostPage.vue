<script setup>
import { ref } from "vue"
import imageDefault from "@/assets/pic/default-featured-image.jpg"

const title = ref("")
const content = ref("")
const imageFile = ref(null) // 用來存放圖片檔案
const previewUrl = ref(imageDefault)
const isEditing = ref(false)
const editIndex = ref(null) //記錄哪一篇正在編輯
const editTemp = ref({}) //暫存編輯的資料

// 顯示
const posts = ref([])

const handleImageUpload = (event) => {
	const file = event.target.files[0]
	if (file) {
		imageFile.value = file
		previewUrl.value = URL.createObjectURL(file) // 生成圖片預覽的URL
	}
}

const submitPost = () => {
	if (isEditing.value && posts.value[editIndex.value]) {
		// 編輯模式下更新:更新指定索引
		posts.value[editIndex.value] = {
			title: title.value,
			content: content.value,
			imageFile: previewUrl.value,
			createdAt: new Date().toLocaleString(),
		}
		isEditing.value = false
		editIndex.value = null
	} else {
		posts.value.push({
			title: title.value,
			content: content.value,
			imageFile: previewUrl.value,
			createdAt: new Date().toLocaleString(), //發布時間
		})
	}
	// 可選：清空表單
	title.value = ""
	content.value = ""
	imageFile.value = null
	previewUrl.value = imageDefault
}
const handleEdit = (index) => {
	const post = posts.value[index]
	title.value = post.title
	content.value = post.content
	previewUrl.value = post.imageFile
	isEditing.value = true
	editIndex.value = index
}
const handleDel = (index) => {
	posts.value.splice(index, 1)
}
</script>
<template>
	<!-- 發文區塊 -->
	<form @submit.prevent="submitPost" class="container w-[700px] p-4 flex flex-col justify-center rounded-lg shadow-md">
		<!-- 發文表單 -->
		<input v-model="title" type="text" placeholder="請輸入文章標題" class="mt bg-white w-[650px] h-[45px]" />
		<textarea
			v-model="content"
			placeholder="請輸入文章內容"
			class="mt w-[650px] h-[120px] bg-white rounded-md shadow-md p-3 resize-none focus:outline-none focus:ring-2 focus:ring-white"
		/>
		<!-- 圖片上傳 -->
		<input type="file" class="mb-2" @change="handleImageUpload" accept="image/*" />
		<!-- 圖片預覽區 -->
		<img :src="previewUrl" class="max-w-full w-[650px] object-contain mb-2 rounded shadow" />
		<button type="submit" class="btn btn-post w-[650px] rounded-lg">發布文章</button>
	</form>
	<div class="line w-[700px] border-b-2 border-gray-300 my-4"></div>

	<!-- 顯示文章 -->
	<div v-for="(post, index) in posts" :key="index" class="container w-[700px] p-4 rounded-lg shadow-md">
		<div class="bg-white w-[650px] flex flex-row justify-between">
			<div class="left">
				<div class="w-full bgc">
					<h1 class="title">{{ post.title }}</h1>
				</div>
				<p class="post-content">{{ post.content }}</p>
			</div>
			<div class="right x border-gray-200">
				<img :src="post.imageFile" alt="圖片" class="mt max-w-full max-h-44 object-contain mb-2 rounded shadow" />
			</div>
		</div>
		<div class="flex justify-between mt">
			<button @click="handleEdit(index)" class="button w-[325px] edit-btn">編輯</button>
			<button @click="handleDel(index)" class="w-[325px] delete-btn">刪除</button>
		</div>
		<p class="text-xs text-gray-500">發布時間：{{ post.createdAt }}</p>
	</div>
</template>

<style>
.edit-btn,
.delete-btn {
	padding: 6px 12px;
	border-radius: 6px;
	border: none;
	cursor: pointer;
	color: white;
}

.edit-btn {
	background-color: #3498db;
}

.delete-btn {
	background-color: #e74c3c;
}
.input,
.textarea,
.file-input {
	padding: 10px;
	font-size: 1rem;
	border: 1px solid #ccc;
	border-radius: 8px;
}
.bgc {
	width: 420px;
	background-color: #f9fafb;
	padding: 3px;
}
.mt {
	margin-top: 10px;
}
.title {
	padding: 8px;
	font-size: 20px;
	font-weight: 700;
	font-weight: bold;
}
.line {
	margin: 0 auto;
}

.container {
	margin: 20px auto;
	padding: 20px;
	background-color: #f9fafb;
}
.btn-post {
	margin-top: 10px;
}
.left {
	padding: 10px;
}

.btn {
	padding: 10px;
	background: #8475b0;
	color: white;
	border: none;
	border-radius: 8px;
	cursor: pointer;
}

.btn:hover {
	background: #6c5da5;
}
</style>
