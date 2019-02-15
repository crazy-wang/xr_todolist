<template>
  <div class="son-com">
    <span class="com-name">{{tipsName}}</span>
    <el-input
      v-if="type === 'input'"
      placeholder="请输入内容"
      v-model="inputValue"
      @blur="changeInput"
      clearable>
    </el-input>
    <el-select v-else v-model="selectValue" clearable placeholder="请选择" @change="changeSelect">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        inputValue: '',
        selectValue: ''
      }
    },
    // tipsName为标题名字
    // type默认为input,决定渲染为输入框还是选择框;
    // 当type为选择框时，需传入resultValueOptions配置项
    // inputValueProp映射inputValue，另一个类似；因为子组件不能直接改父prop传过来的值
    props: {
      tipsName: String,
      type: {
        type: String,
        default: 'input'
      },
      options: Array,
      inputValueProp: String,
      selectValueProp: [String, Number],
    },
    // 监听传入的prop绑定值来和重新赋值给子组件自己的绑定值
    watch: {
      inputValueProp: function (nVal, oVal) {
        this.inputValue = nVal
      },
      selectValueProp: function (nVal, oVal) {
        this.selectValue = nVal
      }
    },
    methods: {
      changeInput() {
        this.$emit('changeInput', this.inputValue)
      },
      changeSelect() {
        this.$emit('changeSelect', this.selectValue)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .son-com {
    margin-bottom: 10px;
    .com-name {
      display: inline-block;
      width: 100px;
      text-align: right;
      margin-right: 10px;
    }
    .el-input, .el-select {
      display: inline-block;
      width: calc(100% - 120px);
    }
  }
</style>
