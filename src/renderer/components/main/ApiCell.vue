<template>
  <div @click.stop="clickInput('edit-remark-input')">
    <el-input v-model="cValue" v-if="this.tableSelected"
              @blur="loseFocus" class="edit-remark-input"
              @input="$emit('input', cValue)"></el-input>
    <span style="margin-left: 10px" v-else>{{ cValue }}</span>
  </div>
</template>

<script>
export default {
  name: "ApiCell",
  props: ['cellValue'],
  data() {
    return {
      tableSelected: false,
      cValue: this.cellValue
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
  padding-left: 10px;
}
</style>
