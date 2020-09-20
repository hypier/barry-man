<template>
  <div>
    <el-row>
      <el-col :span="24">
        <el-link icon="el-icon-caret-right" :underline="false">编辑</el-link>
      </el-col>
    </el-row>
    <el-row type="flex" justify="start">
      <el-col :span="24">
        <el-input placeholder="请输入请求URL" v-model="input">
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
      </el-col>
      <el-col style="min-width: 205px; width: 205px">
        <div>
          <el-button type="primary" style="margin-left: 10px">发送<i class="el-icon-position el-icon--right"></i>
          </el-button>
          <el-button type="info" style="margin-left: 6px">保存<i class="el-icon-finished el-icon--right"></i>
          </el-button>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col>
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane label="Query" name="query"></el-tab-pane>
          <el-tab-pane label="Authorization" name="auth"></el-tab-pane>
          <el-tab-pane label="Header" name="header"></el-tab-pane>
          <el-tab-pane label="Body" name="body"></el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
    <el-row>
      <el-col>
        <div class="title" style="margin-bottom: 5px">Query Params</div>
        <el-table :data="tableData" border style="width: 100%" :show-header="false"
                  :row-style="{height:'32px'}"
                  :cell-style="{padding:0, height: '35px', lineHeight:'35px'}">
          <el-table-column width="40">
            <template scope="scope">
              <el-checkbox v-model="scope.row.seed"></el-checkbox>
            </template>
          </el-table-column>
          <el-table-column label="时间">
            <template scope="scope">
              <ApiCell v-model="scope.row.date" :scope="scope" @change="cellInput"></ApiCell>
            </template>
          </el-table-column>
          <el-table-column label="参数名">
            <template scope="scope">
              <ApiCell v-model="scope.row.name" :scope="scope"></ApiCell>
            </template>
          </el-table-column>
          <el-table-column label="参数值">
            <template scope="scope">
              <ApiCell v-model="scope.row.address" :scope="scope"></ApiCell>
            </template>
          </el-table-column>
        </el-table>
      </el-col>
    </el-row>
  </div>

</template>
<script>
import ApiCell from "./ApiCell";

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
      input: '',
      activeName: 'second',
      tableSelected: {
        index: 0,
        label: ''
      },
      tableData: [{
        seed: true,
        date: '2016-05-02',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        seed: true,
        date: '2016-05-04',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        seed: true,
        date: '2016-05-01',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        seed: true,
        date: '2016-05-03',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1516 弄'
      }]
    }
  },
  created() {
    this.handleAdd()
  },
  methods: {
    handleClick(tab, event) {
      console.log(this.tableData[0].name)
      console.log(tab, event);
    },
    handleAdd() {
      this.tableData.push({isNew: true})
    },
    cellInput(val, scope){
      this.tableData[scope.$index].isNew = !!this.isNew(scope.row);
    },
    isNew(row){
      return this.isEmpty(row.date) && this.isEmpty(row.name) && this.isEmpty(row.address);
    },
    isEmpty(obj){
      if (obj === undefined){
        return true
      }

      return obj.length <= 0;
    }
  },
  components: {
    ApiCell
  },
}
</script>

<style scoped>
.title {
  color: #606266;
  font-size: 13px;
  font-weight: bold;
}

</style>
