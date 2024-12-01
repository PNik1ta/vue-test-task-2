<script setup lang="ts">
import { VueFinalModal } from 'vue-final-modal'
import { IProduct } from '../interfaces/product.interface';
import { useCartStore } from '../store/cart';

const props = defineProps<{
	title?: string
	product: IProduct
}>()

const cartStore = useCartStore();

const addToCart = () => {
  cartStore.addToCart(props.product);
};

const emit = defineEmits<{
	(e: 'confirm'): void
}>()
</script>

<template>
	<VueFinalModal class="confirm-modal" content-class="confirm-modal-content" overlay-transition="vfm-fade"
		content-transition="vfm-fade">
		<div class="modal__header">
			<h3>{{ product.title }}</h3>
			<img @click="emit('confirm')" class="cross" src="@/assets/images/cross.svg" alt="cross icon">
		</div>

		<div class="modal__body">
			<img class="image" :src="product.image" alt="product image">

			<div class="modal__content">
				<div class="content__item">
					<span>Описание</span>
					<p>{{ product.description }}</p>
				</div>

				<div class="content__item">
					<span>Категория</span>
					<p>{{ product.category }}</p>
				</div>

				<div class="content__item">
					<span>Рейтинг</span>
					<p>{{ product.rating.rate }}</p>
				</div>

				<p class="price">{{ product.price }} руб.</p>
				<button @click="addToCart">Купить</button>
			</div>
		</div>
	</VueFinalModal>
</template>

<style>
.confirm-modal {
	display: flex;
	justify-content: center;
	align-items: center;
}

.confirm-modal-content {
	background: #fff;
	width: 954px;
	height: 662px;
}

.modal__header {
	height: 120px;
	background-color: #275742;
	padding: 40px;
	display: flex;
	justify-content: space-between;
}

.modal__header h3 {
	font-size: 32px;
	line-height: 1.15;
	font-weight: 70;
	color: #fff;
}

.modal__header .cross {
	width: 40px;
	height: 40px;
	object-fit: cover;
	cursor: pointer;
}

.modal__body {
	display: flex;
	column-gap: 40px;
	align-items: center;
	padding: 40px;
	height: 542px;
}

.modal__body .image {
	width: 462px;
	height: 462px;
	object-fit: cover;
}

.content__item:not(:last-child) {
	margin-bottom: 12px;
}

.content__item span {
	display: inline-block;
	font-size: 20px;
	line-height: 1.15;
	color: #606462;
	font-weight: 500;
	margin-bottom: 8px;
}

.content__item p {
	font-size: 24px;
	line-height: 1.15;
	font-weight: 500;
	color: #275742;
	max-height: 120px;
	overflow: auto;
}

.price {
	margin-top: 88px;
	font-size: 36px;
	line-height: 1.15;
	font-weight: 700;
	color: #275742;
	margin-bottom: 24px;
}

.modal__content button {
	width: 100%;
	height: 52px;
	background: #275742;
	color: #fff;

	font-size: 24px;
	line-height: 1;
	font-weight: 500;
	transition: all .3s ease 0s;
	cursor: pointer;

	display: flex;
	justify-content: center;
	align-items: center
}

.modal__content button:hover {
	background: #163427;
}
</style>