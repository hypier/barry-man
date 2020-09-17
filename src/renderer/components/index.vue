<template>
  <el-container>
    <el-header style="text-align: right;">
      <el-dropdown>
        <i class="el-icon-setting" style="margin-right: 15px"></i>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>查看</el-dropdown-item>
          <el-dropdown-item>新增</el-dropdown-item>
          <el-dropdown-item>删除</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
      <span>Wang Xiang Hu</span>
    </el-header>
    <el-container>
      <el-aside width="auto">
        <el-row v-show="!isCollapse">
          <el-col>
            <div class="grid-content bg-purple-dark centerClass">
              <el-input placeholder="请输入关键字" v-model="search_input" suffix-icon="el-icon-search"
                        class="searchClass" clearable style="width: 85%">
              </el-input>

            </div>
            <div class="line"></div>
          </el-col>
        </el-row>
        <MenuBar></MenuBar>

      </el-aside>
      <el-main>
        <el-table :data="tableData">
          <el-table-column prop="date" label="日期" width="140">
          </el-table-column>
          <el-table-column prop="name" label="姓名" width="120">
          </el-table-column>
          <el-table-column prop="address" label="地址">
          </el-table-column>
        </el-table>
      </el-main>

    </el-container>
    <el-footer style="height: 30px;line-height: 30px">
      <el-switch
          v-model="isCollapse"
          active-color="#13ce66"
          inactive-color="#ff4949">
      </el-switch>
      <span style="font-size: 12px">展开/收起</span>
    </el-footer>
  </el-container>
</template>

<style type="text/css">

html, body, #app, .el-container {
  /*设置内部填充为0，几个布局元素之间没有间距*/
  padding: 0;
  /*外部间距也是如此设置*/
  margin: 0;
  /*统一设置高度为100%*/
  height: 100%;
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}

.centerClass {
  text-align: center;
}

.el-aside {
  border-right: #e6e6e6 1px solid;
}

.line {
  margin-top: 5px;
  border-bottom: #e6e6e6 1px solid;
}

.el-header {
  background-color: #303133;
  color: #FFF;
  line-height: 60px;
}

.el-aside {
  color: #333;
}

.el-footer {
  border: 1px solid #eee;
  color: #909399;
}

.searchClass {
  border: 1px solid #E4E7ED;
  border-radius: 15px;
  background: #f4f4f4;
  margin: 15px 5px 5px;
}

.searchClass .el-input-group__prepend {
  border: none;
  background-color: transparent;
}

.searchClass .el-input-group__append {
  border: none;
  background-color: transparent;
}

.searchClass .el-input__inner {
  height: 30px;
  line-height: 30px;
  border: none;
  background-color: transparent;
}

.searchClass .el-input__icon {
  line-height: 33px;
}

.searchClass .el-icon-search {
  font-size: 12px;
}

.searchClass .centerClass {
  display: inline-block;
  vertical-align: middle;
  text-align: right;
}

</style>


<script>
import MenuBar from './menu/MenuBar'

export default {

  data() {
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    };
    return {
      tableData: Array(20).fill(item),
      isCollapse: false,
      search_input: ''
    }
  },
  components: {
    MenuBar
  }
};


</script>

