<template>
  <div>
    <div class="bottom-line">
      <el-link icon="el-icon-caret-right" :underline="false">编辑</el-link>
    </div>
    <div style="margin-top: 10px">
      <el-input placeholder="请输入请求URL" v-model="input" style="float: left; width: 90%">
        <div slot="prepend">
          <div class="centerClass">
            <el-select v-model="value" style="width: 100px">
              <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value">
              </el-option>
            </el-select>
          </div>
          <div class="centerClass">
            <div class="line"></div>
          </div>
        </div>
      </el-input>
      <el-button type="primary" style="margin-left: 8px">请求<i class="el-icon-position el-icon--right"></i></el-button>
    </div>

  </div>
</template>
<script>
export default {
  name: "ApiTable",
  data() {
    return {
      options: [{
        value: 'GET',
        label: 'GET'
      }, {
        value: 'POST',
        label: 'POST'
      }, {
        value: 'PUT',
        label: 'PUT'
      }, {
        value: 'PATCH',
        label: 'PATCH'
      }, {
        value: 'DELETE',
        label: 'DELETE'
      }],
      value: 'GET',
      input: ''
    }
  }
}
</script>

<style scoped>

</style>
