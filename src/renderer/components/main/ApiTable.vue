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
        <el-table :data="tableData" border style="width: 100%"
                  :header-cell-style="{padding:0, height: '35px', lineHeight:'35px'}"
                  :row-style="{height:'32px'}"
                  :cell-style="{padding:0, height: '35px', lineHeight:'35px'}">
            <el-table-column width="40">
              <template scope="scope">
                <el-checkbox v-model="scope.row.seed"></el-checkbox>
              </template>
            </el-table-column>
            <el-table-column label="姓名">
              <template scope="scope">
                <div @click.stop="clickInput(scope.$index, scope.column.label, 'edit-remark-input')">
                  <el-input v-model="scope.row.name" v-if="selected(scope.$index, scope.column.label)"
                            @blur="loseFocus(scope.$index, scope.row)" class="edit-remark-input"></el-input>
                  <span style="margin-left: 10px" v-else>{{ scope.row.name }}</span>
                </div>
              </template>
            </el-table-column>
            <el-table-column label="地址">
              <template scope="scope">
                <div @click.stop="clickInput(scope.$index, scope.column.label, 'edit-remark-input')">
                  <el-input v-model="scope.row.address" v-if="selected(scope.$index, scope.column.label)"
                            @blur="loseFocus(scope.$index, scope.row)" class="edit-remark-input"></el-input>
                  <span style="margin-left: 10px" v-else>{{ scope.row.address }}</span>
                </div>
              </template>
            </el-table-column>
        </el-table>
      </el-col>
    </el-row>
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
      }, {
        seed: false,
        date: '1',
        name: '',
        address: ''
      }
      ]
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    },
    loseFocus(index, row) {
      debugger
      row.seen = false;
    },
    clickInput(index, label, className) {
      console.log(label, index, className)
      this.tableSelected = {index: index, label: label}
      //让input自动获取焦点
      this.$nextTick(function () {
        let editInputList = document.getElementsByClassName(className);
        if (editInputList) {
          editInputList[0].children[0].focus();
        }
      });
    },
    selected(index, label) {
      return this.tableSelected.index === index && this.tableSelected.label === label;
    },
  }
}
</script>

<style scoped>
.title {
  color: #606266;
  font-size: 13px;
  font-weight: bold;
}

.edit-remark-input >>> .el-input__inner {
  height: 30px;
  line-height: 30px;
  border: none;
  border-radius: 0;
  padding-left: 10px;
}

</style>
