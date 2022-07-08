<template>
    <div class='container'>
        <div class='container__header'>
            <p class='header__title'>Добавление товара</p>
            <select-button :action='onSelectSorting'/>
        </div>
        <div class='container__content'>
            <div class='content__sidebar'>
                <add-product-form :onCreateProduct='onCreateProduct'/>
            </div>
            <div class='content__products'>
              <transition-group
                v-if='products.length'
                name='products'
                tag='div'
                class='products__group'
              >
                <product-card
                  :onDelete='onDeleteProduct'
                  v-for='product in products'
                  :key='product.id'
                  :product='product'
                />
              </transition-group>
              <p v-else class='products__empty'>Товары не найдены</p>
            </div>
        </div>
    </div>
</template>

<script>
import Select from './Select.vue';
import Form from './Form.vue';
import ProductCard from './ProductCard.vue';

export default {
  components: {
    'select-button': Select,
    'add-product-form': Form,
    'product-card': ProductCard,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    const check = localStorage.getItem('products');
    if (check) {
      this.products = JSON.parse(check);
    } else {
      this.products = [];
    }
  },
  methods: {
    onSelectSorting(value) {
      let sortFunction = () => {};
      if (value === 'name') {
        sortFunction = (firstItem, secondItem) => (firstItem.name > secondItem.name ? 1 : -1);
      } else if (value === 'maxPrice') {
        sortFunction = (firstItem, secondItem) => +firstItem.price - +secondItem.price;
      } else {
        sortFunction = (firstItem, secondItem) => +secondItem.price - +firstItem.price;
      }

      this.products = this.products.sort(sortFunction);
    },
    onCreateProduct(product) {
      const newProduct = {
        id: new Date().getTime().toString(),
        name: product.name.value,
        description: product.description.value,
        image: product.link.value,
        price: product.price.value,
      };
      this.products.push(newProduct);
      localStorage.setItem('products', JSON.stringify(this.products));
    },
    onDeleteProduct(id) {
      this.products = this.products.filter((product) => product.id !== id);
      localStorage.setItem('products', JSON.stringify(this.products));
    },
  },
};
</script>

<style lang='scss' scoped>
.container {
    padding: 32px 32px 0px;
    width: 100%;
    margin: 0 auto;
    max-width: 1460px;

    @media (max-width: 800px) {
        padding: 16px;
    }
}

.container__header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: 16px;

    @media (max-width: 800px) {
        flex-direction: column;
    }
}

.container__content {
    display: flex;
    flex-direction: row;

    @media (max-width: 800px) {
        flex-direction: column;
    }
}

.header__title {
    color: #3F3F3F;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
}

.content__products {
  flex: 1;
  position: relative;
}
.products__group {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(auto-fit, 332px);
  grid-gap: 16px;
  height: 100%;
  max-height: calc(100vh - 100px);
  overflow-y: auto;
  overflow-x: hidden;
  justify-content: center;

  @media (max-width: 800px) {
    margin-top: 16px;
    grid-template-columns: repeat(auto-fit, 100%);
  }
}

.products__group::-webkit-scrollbar {
  width: 0;
}

.products__empty {
  flex: 1;
  text-align: center;
}
</style>
