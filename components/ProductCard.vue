<template>
  <div class='product-container'>
    <div v-on:click='() => onDelete(product.id)' class='container__delete-button'>
      <div class='delete-button__icon'></div>
    </div>
    <img :src='product.image' :alt='product.name' class='container__image'/>
    <div class='container__info'>
      <p class='info__name'>{{ product.name }}</p>
      <p class='info__description'>{{ product.description }}</p>
      <p class='info__price'>{{ priceTransformed }} руб.</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: Object,
    onDelete: Function,
  },
  computed: {
    priceTransformed() {
      return this.product.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
  },
};
</script>

<style lang='scss' scoped>
.product-container {
  transition: all 1s;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  cursor: pointer;
  position: relative;

  &:hover {
    .container__delete-button {
      display: block;
    }
  }
}
.container__delete-button {
  display: none;
  position: absolute;
  width: 32px;
  height: 32px;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  padding: 8px;
  top: 0px;
  right: -8px;

  @media (max-width: 800px) {
    right: 4px;
  }
}
.delete-button__icon {
  width: 13px;
  height: 16px;
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  background-image: url('~/assets/img/delete.png');
}

.container__image {
  object-fit: contain;
  width: 100%;
  height: 200px;
}
.container__info {
  padding: 16px;
}
.info__name {
  font-weight: 600;
  font-size: 20px;
  color: #3f3f3f;
  margin-bottom: 16px;
  overflow: hidden;
  text-overflow: ellipsis;
}
.info__description {
  font-weight: 400;
  font-size: 16px;
  color: #3f3f3f;
  margin-bottom: 32px;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
