<template>
  <div class="wrapper">
    <Header />
    <section class="main">
      <img class="main__image" src="@/assets/images/content.png" alt="content" />
      <img class="main__overlay" src="@/assets/images/content-overlay.png" alt="content overlay" />
    </section>

    <h2 class="section-title">Новинки</h2>
    <section class="products">
      <Product 
        v-for="product in products" 
        :key="product.id" 
        :product="product"
      />
    </section>

    <Footer/>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import Product from '@/components/Product.vue';
import { IProduct } from '../interfaces/product.interface';

export default defineComponent({
  name: 'HomeView',
  components: { Header, Product, Footer },
  
  setup() {
    const products = ref<IProduct[]>([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        const data: IProduct[] = await response.json();
        products.value = data; 
      } catch (error) {
        console.error('Ошибка при загрузке продуктов:', error);
      }
    };

    onMounted(() => {
      fetchProducts();
    });

    return {
      products,
    };
  }
});
</script>

<style>

.wrapper {
  padding: 24px 40px;
}
.main {
  width: 1200px;
  height: 573px;
  position: relative;

  margin: 0 auto;
  margin-top: 12px;
  margin-bottom: 84px;
}

.main__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.main__overlay {
  position: absolute;
  bottom: 0;
  right: 35px;
}


.section-title {
  font-size: 48px;
  line-height: 1.15;
  color: #275742;
  font-weight: 500;
  text-align: center;
  margin-bottom: 40px;
}

.products {
  margin-top: 40px;
  display: grid;
  column-gap: 30px;
  row-gap: 32px;
  grid-template-columns: repeat(3, 380px);
  justify-content: center;
  margin-bottom: 100px;
}
</style>
