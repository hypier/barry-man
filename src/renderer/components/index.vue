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
      <span>Barry的异想世界</span>
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
            <div class="bottom-line"></div>
          </el-col>
        </el-row>
        <MenuBar :collapse="isCollapse"></MenuBar>

      </el-aside>
      <el-main>
        <el-tabs v-model="editableTabsValue" type="card" @tab-remove="removeTab" @tab-click="handleClick">
          <el-tab-pane
              v-for="(item, index) in editableTabs"
              :key="item.name"
              :label="item.title"
              :name="item.name"
              :closable="item.closable">
            <component :is="item.content" v-if="item.content === 'MTable'"></component>
            <api-table v-else></api-table>
          </el-tab-pane>
          <el-tab-pane key="add" name="add" :closable="false" label="+"></el-tab-pane>
        </el-tabs>

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
.bottom-line {
  border-bottom: #e6e6e6 1px solid;
  padding-bottom: 5px;
}

.el-header {
  background-color: #303133;
  color: #FFF;
  line-height: 60px;
}

.el-menu--collapse {
  width: 53px;
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
import MTable from './main/MTable'
import ApiTable from "./main/ApiTable";

export default {

  data() {

    return {
      isCollapse: false,
      search_input: '',

      editableTabsValue: '1',
      editableTabs: [{
        title: 'Tab 1',
        name: '1',
        content: 'Tab 1 content',
        closable: true
      }, {
        title: '表格',
        name: '2',
        content: 'MTable',
        closable: true,
      }
      ],
      tabIndex: 2
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
      if (tab.name === 'add') {
        event.preventDefault()
        this.addTab(this.editableTabsValue)
      }
    },
    addTab(targetName) {
      let newTabName = ++this.tabIndex + '';
      this.editableTabs.push({
        title: 'New Tab',
        name: newTabName,
        content: 'New Tab content',
        closable: true
      });
      this.editableTabsValue = newTabName;
    },
    removeTab(targetName) {
      let tabs = this.editableTabs;
      let activeName = this.editableTabsValue;
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1];
            if (nextTab) {
              activeName = nextTab.name;
            }
          }
        });
      }

      this.editableTabsValue = activeName;
      this.editableTabs = tabs.filter(tab => tab.name !== targetName);
    }
  },
  components: {
    MenuBar,
    MTable,
    ApiTable
  }
};


</script>

