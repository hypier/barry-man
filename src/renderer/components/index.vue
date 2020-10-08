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
        <MenuBar :collapse="isCollapse" :menuData="this.requestData" @select="handleSelect"></MenuBar>

      </el-aside>
      <el-main style="padding: 10px">
        <ApiTabs v-model="tabsData"></ApiTabs>
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
import ApiTabs from "./main/ApiTabs";

export default {

  data() {

    return {
      isCollapse: false,
      search_input: '',
      requestData: [],
      tabsData: [],
    }
  },
  created: function () {
    this.getData()
  },
  methods: {
    getData: function () {
      let fs = require('fs'),
          Collection = require('postman-collection').Collection,
          path = require('path'),
          myCollection;

      myCollection = new Collection(JSON.parse(fs.readFileSync(
          path.resolve(__dirname, '../../docs/doc.postman_collection.json')).toString()));

      let json = myCollection.toJSON()

      this.requestData.push({
        items: json.item,
        info: json.info
      })

      //this.addData(json.item)
    },
    addData(items) {
      for (let i = 0; i < items.length; i++) {
        let obj = items[i]
        if (obj.request) {
          this.tabsData.push(obj)
        }

        if (obj.item) {
          this.addData(obj.item)
        }
      }
    },
    handleSelect: function (key, keyPath) {
      console.log(key, keyPath)
    }
  },
  components: {
    ApiTabs,
    MenuBar
  }
};


</script>

