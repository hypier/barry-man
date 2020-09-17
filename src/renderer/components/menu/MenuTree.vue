<template>
  <div>
    <template v-for="value in this.menuData">
      <el-submenu :index="value.name" v-if="value.item">
        <template slot="title">
          <i class="el-icon-folder-add"></i>
          <span slot="title">{{ value.name }}</span>
        </template>
        <MenuTree :menuData="value.item"></MenuTree>
      </el-submenu>
      <el-menu-item index="value.name" v-else>
        <i class="el-icon-s-order"></i>
        <span slot="title">{{ value.name }}</span>
      </el-menu-item>
    </template>
  </div>
</template>

<script>
export default {
  props: ['menuData'],
  name: 'MenuTree',
}
</script>
