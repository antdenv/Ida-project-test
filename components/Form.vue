<template>
  <div class='form'>
    <div class='form__container' v-if='!isComplete'>
        <form-input
            :info='formInfo.name'
            field='name'
            placeholder='Наименование товара'
            title='Наименование товара'
            type='text'
            :action='onChange'
            isRequired
        />
        <form-input
            :info='formInfo.description'
            field='description'
            placeholder='Описание товара'
            title='Описание товара'
            type='text'
            :action='onChange'
            isDescription
        />
        <form-input
            :info='formInfo.link'
            field='link'
            placeholder='Ссылка на изображение товара'
            title='Ссылка на изображение товара'
            type='text'
            :action='onChange'
            isRequired
        />
        <form-input
            :info='formInfo.price'
            field='price'
            placeholder='Цена'
            title='Цена товара'
            type='number'
            :action='onChange'
            isRequired
        />
        <form-button
            :action='addProduct'
            :isValid='isValid'
            title='Добавить товар'
        />
    </div>
    <div class='form__complete' v-else>
      <div class='complete__icon'></div>
      <p class='complete__message'>Товар успешно добавлен</p>
    </div>
  </div>
</template>

<script>
import Input from './Input.vue';
import Button from './Button.vue';

export default {
  components: {
    'form-input': Input,
    'form-button': Button,
  },
  props: {
    onCreateProduct: Function,
  },
  data() {
    return {
      formInfo: {
        name: {
          isError: false,
          value: '',
        },
        description: {
          isError: false,
          value: '',
        },
        link: {
          isError: false,
          value: '',
        },
        price: {
          isError: false,
          value: '',
        },
      },
      isValid: false,
      isComplete: false,
    };
  },
  methods: {
    onChange(type, value) {
      this.formInfo[type] = {
        isError: type !== 'description' && value === '',
        value,
      };
      this.isValid = Object.keys(this.formInfo).every(
        (key) => this.formInfo[key].value !== '' || key === 'description',
      );
    },
    addProduct() {
      this.onCreateProduct(this.formInfo);
      Object.keys(this.formInfo).forEach((key) => {
        this.formInfo[key] = { isError: false, value: '' };
      });
      this.isValid = false;
      this.isComplete = true;
      setTimeout(() => { this.isComplete = false; }, 2000);
    },
  },
};
</script>

<style lang='scss' scoped>
.form__container, .form__complete {
  width: 332px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  margin-right: 16px;

  @media (max-width: 800px) {
    width: 100%;
    margin-bottom: 15px;
  }
}

.form__complete {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: 0.55s opacity, 0.55s visibility;
}

.complete__icon {
  width: 50px;
  height: 50px;
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  background-image: url('~/assets/img/mark.jpg');
  margin-bottom: 10px;
}
</style>
