<template>
  <div @click.stop="clickInput('edit-remark-input')"
       style="width: 100%;line-height: 35px;height: 35px">
    <el-input v-model="cValue" v-if="this.tableSelected"
              @blur="loseFocus" class="edit-remark-input"
              @input="$emit('input', cValue)"
              @change="$emit('change', cValue, scope)" clearable></el-input>
    <span v-else-if="scope.row.isNew" style="color: #909399">{{ scope.column.label }}</span>
    <span v-else style="color: #303133">{{ cValue }}</span>
  </div>
</template>

<script>
export default {
  name: "ApiCell",
  props: {
    value: {
      type: String
    },
    scope: {
      type: Object
    }
  },
  data() {
    return {
      tableSelected: false,
      cValue: this.value
    }
  },
  methods: {
    loseFocus() {
      this.tableSelected = false
    },
    clickInput(className) {
      console.log(className)
      this.tableSelected = true
      //让input自动获取焦点
      this.$nextTick(function () {
        let editInputList = document.getElementsByClassName(className);
        if (editInputList.length > 0) {
          editInputList[0].children[0].focus();
        }
      });
    },
  }
}
</script>

<style scoped>
.edit-remark-input >>> .el-input__inner {
  height: 30px;
  line-height: 30px;
  border: none;
  border-radius: 0;
  padding-left: 0;
  color: #303133;
}
</style>
