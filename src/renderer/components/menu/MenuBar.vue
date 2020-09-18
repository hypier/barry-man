<template>
  <el-menu class="el-menu-vertical" @open="handleOpen" @close="handleClose"
           :collapse="this.collapse" style="border-right: none;">
    <MenuTree :menuData="this.menuData"></MenuTree>
  </el-menu>
</template>

<script>
import MenuTree from './MenuTree'

export default {
  props: ['collapse'],
  data() {
    return {
      menuData: []
    }
  },
  created: function () {
    this.getMenu()
  },
  methods: {
    handleOpen(key, keyPath) {
      event.target.parentElement.getElementsByClassName("el-icon-folder-add")[0]
          .setAttribute("class", "el-icon-folder-opened")
    },
    handleClose(key, keyPath) {
      event.target.parentElement.getElementsByClassName("el-icon-folder-opened")[0]
          .setAttribute("class", "el-icon-folder-add")
    },
    getMenu: function () {
      let fs = require('fs'),
          path = require('path'),
          myCollection;

      myCollection = JSON.parse(fs.readFileSync(
          path.resolve(__dirname, '../../../docs/doc.postman_collection.json')).toString());
      this.menuData = myCollection.item
    }
  },
  components: {
    MenuTree
  }
}
</script>
<style type="text/css">

.el-menu-vertical:not(.el-menu--collapse) {
  width: 250px;
}

.el-menu--collapse .el-submenu__title span {
  height: 0;
  width: 0;
  overflow: hidden;
  visibility: hidden;
  display: inline-block;
}

.el-submenu .el-menu-item {
  height: 30px !important;
  line-height: 30px !important;
}

.el-menu--collapse .el-submenu__icon-arrow {
  display: none;
}
</style>
