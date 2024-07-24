<template>
    <div class="home-page">
        <div class="home-page__filters">
            <filter-box />
        </div>
        <div class="home-page__products">
            <product-card
                v-for="product in products"
                :key="product.id"
                :brand="product.brand"
                :name="product.name"
                :price="product.price"
                :oldPrice="product.oldPrice"
                :hit="product.hit"
                :discount="product.discount"
                :stock="product.stock"
            />
        </div>
    </div>
</template>

<script>
import FilterBox from '../components/FilterBox.vue';
import ProductCard from '../components/ProductCard.vue';

export default {
  components: { 
    FilterBox,
    ProductCard 
  },
  data() {
    return {
      products: [
        { id: 1, brand: 'Бренд 1', price: '4 990', oldPrice: '5 990', hit: true, discount: 20, stock: true },
        { id: 2, brand: 'Бренд 2', name: 'Название товара 2', stock: false },
        { id: 3, brand: 'Бренд 3', name: 'Название товара 3', price: '6 990', hit: true, stock: true },
        { id: 4, brand: 'Бренд 4', name: 'Название товара 4', price: '2 990', oldPrice: '3 990', hit: false, discount: 15, stock: true },
        { id: 5, brand: 'Бренд 5', name: 'Название товара 5', price: '8 990', oldPrice: '9 990', hit: true, discount: 25, stock: true },
        { id: 6, brand: 'Бренд 6', name: 'Название товара 6', stock: false },
        { id: 7, brand: 'Бренд 7', name: 'Название товара 7', price: '7 990', oldPrice: '8 990', hit: true, discount: 40, stock: true },
        { id: 8, brand: 'Бренд 8', name: 'Название товара 8', price: '1 990', oldPrice: '2 990', hit: false, discount: 50, stock: true },
        { id: 9, brand: 'Бренд 9', name: 'Название товара 9', price: '6 490', oldPrice: '7 490', hit: true, discount: 35, stock: true },
        { id: 10, brand: 'Бренд 10', name: 'Название товара 10', price: '9 990', oldPrice: '10 990', hit: true, discount: 45, stock: true },
        { id: 11, brand: 'Бренд 11', stock: false },
        { id: 12, brand: 'Бренд 12', name: 'Название товара 12', price: '4 490', oldPrice: '5 490', hit: true, discount: 20, stock: true }
      ]
    }
  },
};
</script>

<style lang="scss" scoped>
  .home-page {
    display: flex;
    gap: 36px;
    &__products {
      width: 100%;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 24px;
    }
  }

  @media (max-width: 1200px) {
    .home-page {
      &__filters {
        display: none;
      }
    }
  }
  
  @media (max-width: 992px) {
    .home-page {
      &__products {
        grid-template-columns: repeat(3, 1fr);
      }
    }
  }

  @media (max-width: 768px) {
    .home-page {
      &__products {
        grid-template-columns: repeat(2, 1fr);
      }
    }
  }
</style>
