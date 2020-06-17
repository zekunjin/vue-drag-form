<template>
  <div class="vue-drag-form-layout">
    <a-row :gutter="16">
      <a-col :span="6">
        <a-card class="select">
          <a-row :gutter="[16,16]">
            <a-col v-for="item of componentsArr" :key="item.key" :span="12">
              <a-card
                hoverable
                draggable="true"
                @dragstart="onDragStart($event, item)"
                @dragend="onDragEnd"
                class="component"
              >{{ item.label }}</a-card>
            </a-col>
          </a-row>
        </a-card>
      </a-col>

      <a-col :span="18">
        <a-card class="overview" @drop="onDrop" @dragover.prevent>
          <a-card v-for="(item, index) in formData" :key="index">
            <div class="form-item">
              <component :is="item.component" :value="item" @add="onAddOption($event, index)" @remove="onRemoveOption($event, index)" />

              <div class="tools">
                <a-icon class="tool-item" type="close" @click="onRemoveItem(index)" />
              </div>
            </div>
          </a-card>
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import Vue from 'vue'
import { Row, Col, Card, Icon } from 'ant-design-vue'
import CInput from './FormItem/CInput'
import CTextarea from './FormItem/CTextarea'
import CSelect from './FormItem/CSelect'
import CRadio from './FormItem/CRadio'

Vue.use(Row)
  .use(Col)
  .use(Card)
  .use(Icon)

const componentsArr = [
  { key: 'INPUT', label: 'input', component: 'c-input' },
  { key: 'TEXTAREA', label: 'textarea', component: 'c-textarea' },
  { key: 'SELECT ', label: 'select', component: 'c-select',  options: [] },
  { key: 'RADIO ', label: 'radio', component: 'c-radio', options: [] }
]

export default {
  components: {
    CInput,
    CTextarea,
    CSelect,
    CRadio
  },

  data() {
    return {
      formData: [],
      componentsArr
    }
  },

  methods: {
    onDragStart(e, item) {
      const value = JSON.stringify(item)
      e.dataTransfer.setData('value', value)
    },

    onDragEnd(e) {
      e.dataTransfer.clearData()
    },

    onDrop(e) {
      const value = JSON.parse(e.dataTransfer.getData('value'))
      this.formData.push(value)
      this.onChange()
    },

    onRemoveItem(index) {
      this.formData.splice(index, 1)
    },

    onAddOption(e, index) {
      this.formData[index].options.push(e)
    },

    onRemoveOption(e, index) {
      this.formData[index].options.splice(e, 1)
    },

    onChange() {
      this.$emit('change', this.formData)
    }
  }
}
</script>

<style lang="less" scoped>
.vue-drag-form-layout {
  padding: 24px;

  .select {
    background-color: rgba(0, 0, 0, 0.05);

    .component {
      height: 48px;
      background-color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
    }
  }

  .overview {
    background-color: rgba(0, 0, 0, 0.05);
    min-height: 512px;

    .form-item {
      display: flex;
      justify-content: space-between;

      .tools {
        .tool-item {
          cursor: pointer;
        }
      }
    }
  }
}
</style>