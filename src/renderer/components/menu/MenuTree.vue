<template>
  <div>

    <el-submenu :index="menuInfo._postman_id" v-if="menuInfo">
      <template slot="title">
        <i class="el-icon-folder-add"></i>
        <span slot="title">{{ menuInfo.name }}</span>
      </template>
      <MenuTree :menuData="this.menuData"></MenuTree>
    </el-submenu>

    <template v-for="value in this.menuData" v-else>
      <el-submenu :index="value.id" v-if="value.item">
        <template slot="title">
          <i class="el-icon-folder-add"></i>
          <span slot="title">{{ value.name }}</span>
        </template>
        <MenuTree :menuData="value.item"></MenuTree>
      </el-submenu>

      <el-menu-item :index="value.id" v-else>
        <i class="el-icon-s-order"></i>
        <span slot="title">{{ value.name }}</span>
      </el-menu-item>
    </template>
  </div>
</template>

<script>
export default {
  props: ['menuData', 'menuInfo'],
  name: 'MenuTree',
}
</script>
