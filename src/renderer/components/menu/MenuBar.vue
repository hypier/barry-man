<template>
  <el-menu class="el-menu-vertical" @open="handleOpen" @close="handleClose" @select="handleSelect"
           :collapse="this.collapse" style="border-right: none;">
    <MenuTree :menuData="this.menuData" :menuInfo="this.menuInfo"></MenuTree>
  </el-menu>
</template>

<script>
import MenuTree from './MenuTree'

export default {
  props: ['collapse'],
  data() {
    return {
      menuData: [],
      menuInfo: {},
      itemData: new Map()
    }
  },
  created: function () {
    this.getMenu()
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(this.itemData.get(key))
    },
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
          Collection = require('postman-collection').Collection,
          path = require('path'),
          myCollection;

      myCollection = new Collection(JSON.parse(fs.readFileSync(
          path.resolve(__dirname, '../../../docs/doc.postman_collection.json')).toString()));

      let json = myCollection.toJSON()
      this.menuData = json.item
      this.menuInfo = json.info
      this.addData(json.item)

    },
    addData(items) {
      for (let i = 0; i < items.length; i++) {
        let obj = items[i]
        if (obj.request) {
          this.itemData.set(obj.id, obj)
        }

        if (obj.item) {
          this.addData(obj.item)
        }
      }

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
