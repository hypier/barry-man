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
                        class="searchClass" clearable style="width: 95%">
              </el-input>

            </div>
            <div class="line"></div>
          </el-col>
        </el-row>
        <el-menu default-active="1-4-1" class="el-menu-vertical" @open="handleOpen" @close="handleClose"
                 :collapse="isCollapse" style="border-right: none;">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span slot="title">导航一</span>
            </template>
            <el-menu-item-group>
              <span slot="title">分组一</span>
              <el-menu-item index="1-1">选项1</el-menu-item>
              <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <span slot="title">选项4</span>
              <el-menu-item index="1-4-1">选项1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-menu-item index="2">
            <i class="el-icon-menu"></i>
            <span slot="title">导航二</span>
          </el-menu-item>
          <el-menu-item index="3" disabled>
            <i class="el-icon-document"></i>
            <span slot="title">导航三</span>
          </el-menu-item>
          <el-menu-item index="4">
            <i class="el-icon-setting"></i>
            <span slot="title">导航四</span>
          </el-menu-item>
        </el-menu>
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

.el-menu-vertical:not(.el-menu--collapse) {
  width: 280px;

}

.searchClass {
  border: 1px solid #c5c5c5;
  border-radius: 15px;
  background: #f4f4f4;
  margin: 5px;
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
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>
