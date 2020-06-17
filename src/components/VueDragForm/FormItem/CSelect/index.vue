<template>
  <div class="select-layout">
    {{ value }}
    <div class="options-content">
      <div class="option-item" v-for="(option, _index) in value.options" :key="_index">
        <a-input v-model="value.options[_index]" :placeholder="`option ${_index + 1}`" />
        <a-icon type="delete" class="remove-icon" @click="onRemoveOption" />
      </div>

      <a-button type="dashed" @click="onAddOption()">add option</a-button>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { Input, Button } from 'ant-design-vue'

Vue.use(Input).use(Button)

export default {
  props: {
    value: {
      type: Object,
      default: () => ({})
    }
  },

  methods: {
    onAddOption() {
      this.$emit('add', '')
    },

    onRemoveOption(index) {
      this.$emit('remove', index)
    }
  }
}
</script>

<style lang="less" scoped>
.select-layout {
  flex: 1;

  .options-content {
    margin-top: 16px;

    .option-item {
      margin: 16px 0;
      display: flex;
      align-items: center;

      .remove-icon {
        margin: 0 16px;
        cursor: pointer;
      }
    }
  }
}
</style>
