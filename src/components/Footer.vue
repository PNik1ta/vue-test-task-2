<template>
	<footer class="footer">
		<h3>Штуки</h3>

		<nav class="footer__links">
			<a>Главная</a>
			<a>Магазин</a>
		</nav>

		<button>Напиши нам</button>

	</footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
	name: 'Footer',
});
</script>

<style scoped>
.footer {
	width: 100%;
	height: 124px;
	background-color: #275742;
	padding: 24px 40px;

	display: flex;
	justify-content: space-between;
	align-items: center;

	margin-bottom: 24px;
}

.footer h3 {
	font-size: 32px;
	line-height: 1.15;
	font-weight: 700;
	color: #fff;
}

.footer__links {
	display: flex;
	column-gap: 32px;
	align-items: center;
}

.footer__links a {
	font-size: 20px;
	color: #fff;
	line-height: 1.15;
	font-weight: 500;
	transition: all .3s ease 0s;
}

.footer__links a:hover {
	color: #bcbaba;
}

.footer button {
	font-size: 20px;
	line-height: 1;
	font-weight: 500;
	color: #fff;
	border: 2px solid #fff;
	border-radius: 2px;
	padding: 12px 16px;

	display: flex;
	justify-content: center;
	align-items: center;

	width: 153px;
	background-color: #275742;
	transition: all .3s ease 0s;
	cursor: pointer;
}

.footer button:hover {
	background-color: #fff;
	color: #275742;
}
</style>