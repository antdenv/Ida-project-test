<template>
    <div class='wrapper'>
        <p v-bind:class="{'wrapper__title': true, required: isRequired}">
            {{title}}
        </p>
        <textarea
          v-if='isDescription'
          v-on:input='onChange'
          v-model='info.value'
          :type='type'
          :class='{input: true, error: info.isError, description: isDescription}'
          :placeholder='placeholder'
        ></textarea>
        <input
            v-on:input='onChange'
            v-model='info.value'
            v-else
            :type='type'
            :class='{input: true, error: info.isError}'
            :placeholder='placeholder'
        />
        <p :class="{'wrapper__error': true, show: info.isError}">
            Поле является обязательным
        </p>
    </div>
</template>

<script>
export default {
  props: {
    placeholder: String,
    title: String,
    type: String,
    field: String,
    info: Object,
    isRequired: {
      type: Boolean,
      default: false,
    },
    isDescription: {
      type: Boolean,
      default: false,
    },
    action: {
      type: Function,
      default: () => {},
    },
  },
  methods: {
    onChange(event) {
      const { value } = event.target;
      this.action(this.field, value);
    },
  },
};
</script>

<style lang='scss' scoped>
.wrapper {
  & * {
    &:not(:last-child) {
      margin-bottom: 4px;
    }
  }
}
.input {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-size: 12px;
  color: #3f3f3f;
  width: 100%;

  &.error {
    border: 1px solid #ff8484;
  }

  &.description {
    height: 108px;
    resize: none;
  }
}
.wrapper__title {
  font-size: 10px;
  color: #49485e;
  display: flex;

  &.required {
    &:after {
      content: '';
      display: block;
      min-width: 4px;
      min-height: 4px;
      width: 4px;
      height: 4px;
      background: #ff8484;
      border-radius: 50%;
    }
  }
}
.wrapper__error {
  font-size: 10px;
  color: #ff8484;
  opacity: 0;

  &.show {
    opacity: 1;
  }
}
</style>
