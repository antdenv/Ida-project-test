<template>
    <div class='wrapper'>
        <button v-on:click='onButtonClick' class='wrapper__select'>
            {{ title }}
        </button>
        <div v-if='isOpen' class='wrapper__options'>
            <p
                class='options__value'
                v-for='option in options'
                :key='option.title'
                v-on:click='onSelectOption(option)'
            >
                {{ option.title }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    action: Function,
  },
  data() {
    return {
      isOpen: false,
      title: 'По умолчанию',
      options: {
        name: {
          value: 'name',
          title: 'По наименованию',
        },
        minPrice: {
          value: 'minPrice',
          title: 'По убыванию цены',
        },
        maxPrice: {
          value: 'maxPrice',
          title: 'По возрастанию цены',
        },
      },
    };
  },
  methods: {
    onButtonClick() {
      this.isOpen = !this.isOpen;
    },
    onSelectOption(option) {
      this.isOpen = false;
      this.title = option.title;
      this.action(option.value);
    },
  },
};
</script>

<style lang='scss' scoped>
.wrapper {
    position: relative;
}

.wrapper__select {
    display: flex;
    flex-direction: row;
    padding: 10px 16px;
    background-color: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #b4b4b4;
    border: none;
    width: 100%;

    &::after {
        content: '';
        background-repeat: no-repeat;
        background-size: contain;
        background-position: center;
        background-image: url('~/assets/img/arrow.png');
        width: 15px;
        height: 10px;
        margin-left: 2px;
        margin-top: 1px;
    }

    @media (max-width: 800px) {
        width: auto;
        margin-top: 12px;
    }
}

.wrapper__options {
    position: absolute;
    z-index: 1;
    top: 35px;
    background-color: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    width: 100%;

    & * {
        cursor: pointer;
        font-size: 12px;

        &:not(:last-child) {
            margin-bottom: 10px;
        }
    }
}
</style>
