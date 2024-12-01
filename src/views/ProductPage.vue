<script lang="ts">
import { defineComponent } from 'vue';
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import { useCartStore } from '@/store/cart';


export default defineComponent({
	name: 'HomeView',
	components: { Header, Footer }, // Добавляем Header в components
	setup: () => {
		const cartStore = useCartStore();

		const removeItem = (id: number) => {
			cartStore.removeFromCart(id);
		}
		return { cartStore, removeItem };
	}
});
</script>

<template>
	<div class="wrapper">
		<Header />
		<h1>Корзина</h1>

		<table class="info" v-if="cartStore.items.length">
			<thead>
				<tr>
					<th>Товар</th>
					<th>Цена, руб</th>
					<th>Кол-во</th>
					<th>Сумма, руб</th>
					<th>Удалить</th>
				</tr>
			</thead>

			<tbody>
				<tr v-for="item in cartStore.items" :key="item.id">
					<td>{{ item.title }}</td>
					<td>{{ item.price }}</td>
					<td>{{ item.quantity }}</td>
					<td>{{ (item.price * item.quantity).toFixed(2) }}</td>
					<td>
            <img @click="removeItem(item.id)" src="@/assets/images/remove.svg" alt="remove icon">
          </td>
				</tr>
				<tr>
					<td>Итог</td>
					<td></td>
					<td>{{ cartStore.totalQuantity }}</td>
					<td>{{ cartStore.totalAmount.toFixed(2) }}</td>
					<td></td>
				</tr>
			</tbody>
		</table>

		<button class="buyAll">Плачу за всё!</button>
		<Footer />
	</div>
</template>

<style scoped>
h1 {
	margin: 40px 0;
	text-align: center;
	font-size: 48px;
	line-height: 1.15;
	color: #275742;
	font-weight: 500;
}

.info {
	width: 100%;
	border: 2px solid #1E4534;
	border-collapse: collapse;
	margin-bottom: 60px;
}

.info thead tr th {
	font-size: 22px;
	line-height: 1.15;
	color: #1E4534;
	font-weight: 700;
	text-align: left;
}

.info tbody tr td {
	font-size: 22px;
	line-height: 1.15;
	font-weight: 50;
	color: #275742;
}

.info tbody tr td {
	padding: 20px 16px;
}

.info thead tr {
	border-bottom: 2px solid #1E4534;
}

.info tbody tr img {
	cursor: pointer;
}

.info thead tr th {
	padding: 20px 16px;

}

.info tbody tr {
	border-bottom: 2px solid #1E4534;
}

.buyAll {
	width: 332px;
	height: 52px;
	display: flex;
	justify-content: center;
	align-items: center;
	margin-bottom: 142px;

	background-color: #275742;
	color: #fff;
	font-size: 24px;
	line-height: 1;
	font-weight: 500;
	transition: all .3s ease 0s;
	cursor: pointer;
	margin-left: auto;
	margin-right: 0;
}

.buyAll:hover {
	background-color: #214436;
}
</style>