<template>
  <el-menu class="el-menu-vertical" @open="handleOpen" @close="handleClose"
           :collapse="isCollapse" style="border-right: none;">
    <MenuTree :menuData="this.menuData"></MenuTree>
  </el-menu>
</template>

<script>
import MenuTree from './MenuTree'

export default {
  data() {
    return {
      isCollapse: false,
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
  width: 280px;
}

</style>
