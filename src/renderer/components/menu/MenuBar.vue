<template>
  <el-menu class="el-menu-vertical" @open="handleOpen" @close="handleClose"
           @select="handleSelect"
           :collapse="this.collapse" style="border-right: none;">
    <template v-for="item in this.menuData">
      <MenuTree :menuData="item.items" :menuInfo="item.info"></MenuTree>
    </template>
  </el-menu>
</template>

<script>
import MenuTree from './MenuTree'

export default {
  props: ['collapse', 'menuData'],

  methods: {
    handleSelect(key, keyPath) {
      this.$emit('select', key, keyPath)
    },
    handleOpen(key, keyPath) {
      event.target.parentElement.getElementsByClassName("el-icon-folder-add")[0]
          .setAttribute("class", "el-icon-folder-opened")
    },
    handleClose(key, keyPath) {
      event.target.parentElement.getElementsByClassName("el-icon-folder-opened")[0]
          .setAttribute("class", "el-icon-folder-add")
    },

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
