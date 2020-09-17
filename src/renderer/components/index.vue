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
        <el-menu default-active="1-4-1" class="el-menu-vertical" @open="handleOpen" @close="handleClose"
                 :collapse="isCollapse" style="border-right: none;" v-for="navMenu in getMenu()">

          <el-submenu v-if="navMenu.childs&&navMenu.entity&&navMenu.entity.state==='ENABLE'"
                      :index="navMenu.entity.index">
            <template slot="title">
              <i :class="navMenu.entity.icon"></i>
              <span slot="title">{{ navMenu.entity.alias }}</span>
            </template>

            <div v-for="subMenu in navMenu.childs">
              <el-submenu v-if="subMenu.childs" :index="subMenu.entity.index">
                <span slot="title">{{ subMenu.entity.alias }}</span>

                <div v-for="m in subMenu.childs">
                  <el-menu-item :index="m.entity.index">
                    {{ m.entity.alias }}
                  </el-menu-item>
                </div>

              </el-submenu>
              <el-menu-item v-else :index="subMenu.entity.index">
                {{ subMenu.entity.alias }}
              </el-menu-item>
            </div>

          </el-submenu>

          <!--          <el-menu-item index="2">-->
          <!--            <i class="el-icon-menu"></i>-->
          <!--            <span slot="title">导航二</span>-->
          <!--          </el-menu-item>-->
          <!--          <el-menu-item index="3" disabled>-->
          <!--            <i class="el-icon-document"></i>-->
          <!--            <span slot="title">导航三</span>-->
          <!--          </el-menu-item>-->
          <!--          <el-menu-item index="4">-->
          <!--            <i class="el-icon-setting"></i>-->
          <!--            <span slot="title">导航四</span>-->
          <!--          </el-menu-item>-->

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

.el-menu-vertical:not(.el-menu--collapse) {
  width: 280px;

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
    },
    getMenu() {
      return [
        {
          "entity": {
            "id": 1,
            "index": "1",
            "parentMenuId": 0,
            "name": "systemManage",
            "icon": "el-icon-message",
            "alias": "系统管理",
            "state": "ENABLE",
            "sort": 0,
            "value": null,
            "type": "NONE",
            "discription": "用于系统管理的菜单",
            "createUserId": 1
          },
          "childs": [
            {
              "entity": {
                "id": 3,
                "parentMenuId": 1,
                "name": "authManage",
                "icon": "el-icon-loading",
                "alias": "权限管理",
                "state": "ENABLE",
                "sort": 0,
                "value": "/system/auth",
                "type": "LINK",
                "discription": "用于权限管理的菜单",
                "createUserId": 1
              },
              "childs": null
            },
            {
              "entity": {
                "id": 4,
                "parentMenuId": 1,
                "name": "roleManage",
                "icon": "el-icon-bell",
                "alias": "角色管理",
                "state": "ENABLE",
                "sort": 1,
                "value": "/system/role",
                "type": "LINK",
                "discription": "用于角色管理的菜单",
                "createUserId": 1
              },
              "childs": null
            },
            {
              "entity": {
                "id": 2,
                "parentMenuId": 1,
                "name": "menuManage",
                "icon": "el-icon-edit",
                "alias": "菜单管理",
                "state": "ENABLE",
                "sort": 2,
                "value": "/system/menu",
                "type": "LINK",
                "discription": "用于菜单管理的菜单",
                "createUserId": 1
              },
              "childs": null
            },
            {
              "entity": {
                "id": 5,
                "parentMenuId": 1,
                "name": "groupManage",
                "icon": "el-icon-mobile-phone\r\n",
                "alias": "分组管理",
                "state": "ENABLE",
                "sort": 3,
                "value": "/system/group",
                "type": "LINK",
                "discription": "用于分组管理的菜单",
                "createUserId": 1
              },
              "childs": null
            }
          ]
        },
        {
          "entity": {
            "id": 6,
            "index": "2",
            "parentMenuId": 0,
            "name": "userManage",
            "icon": "el-icon-news",
            "alias": "用户管理",
            "state": "ENABLE",
            "sort": 1,
            "value": null,
            "type": "NONE",
            "discription": "用于用户管理的菜单",
            "createUserId": 1
          },
          "childs": [
            {
              "entity": {
                "id": 7,
                "parentMenuId": 6,
                "name": "accountManage",
                "icon": "el-icon-phone-outline\r\n",
                "alias": "帐号管理",
                "state": "ENABLE",
                "sort": 0,
                "value": "",
                "type": "NONE",
                "discription": "用于帐号管理的菜单",
                "createUserId": 1
              },
              "childs": [
                {
                  "entity": {
                    "id": 14,
                    "parentMenuId": 7,
                    "name": "emailManage",
                    "icon": "el-icon-sold-out\r\n",
                    "alias": "邮箱管理",
                    "state": "ENABLE",
                    "sort": 0,
                    "value": "/content/email",
                    "type": "LINK",
                    "discription": "用于邮箱管理的菜单",
                    "createUserId": 1
                  },
                  "childs": null
                },
                {
                  "entity": {
                    "id": 13,
                    "parentMenuId": 7,
                    "name": "passManage",
                    "icon": "el-icon-service\r\n",
                    "alias": "密码管理",
                    "state": "ENABLE",
                    "sort": 1,
                    "value": "/content/pass",
                    "type": "LINK",
                    "discription": "用于密码管理的菜单",
                    "createUserId": 1
                  },
                  "childs": null
                }
              ]
            },
            {
              "entity": {
                "id": 8,
                "parentMenuId": 6,
                "name": "integralManage",
                "icon": "el-icon-picture",
                "alias": "积分管理",
                "state": "ENABLE",
                "sort": 1,
                "value": "/user/integral",
                "type": "LINK",
                "discription": "用于积分管理的菜单",
                "createUserId": 1
              },
              "childs": null
            }
          ]
        },
        {
          "entity": {
            "id": 9,
            "index": "3",
            "parentMenuId": 0,
            "name": "contentManage",
            "icon": "el-icon-rank",
            "alias": "内容管理",
            "state": "ENABLE",
            "sort": 2,
            "value": null,
            "type": "NONE",
            "discription": "用于内容管理的菜单",
            "createUserId": 1
          },
          "childs": [
            {
              "entity": {
                "id": 10,
                "parentMenuId": 9,
                "name": "classifyManage",
                "icon": "el-icon-printer",
                "alias": "分类管理",
                "state": "ENABLE",
                "sort": 0,
                "value": "/content/classify",
                "type": "LINK",
                "discription": "用于分类管理的菜单",
                "createUserId": 1
              },
              "childs": null
            },
            {
              "entity": {
                "id": 11,
                "parentMenuId": 9,
                "name": "articleManage",
                "icon": "el-icon-star-on",
                "alias": "文章管理",
                "state": "ENABLE",
                "sort": 1,
                "value": "/content/article",
                "type": "LINK",
                "discription": "用于文章管理的菜单",
                "createUserId": 1
              },
              "childs": null
            },
            {
              "entity": {
                "id": 12,
                "parentMenuId": 9,
                "name": "commentManage",
                "icon": "el-icon-share",
                "alias": "评论管理",
                "state": "ENABLE",
                "sort": 2,
                "value": "/content/comment",
                "type": "LINK",
                "discription": "用于评论管理的菜单",
                "createUserId": 1
              },
              "childs": null
            }
          ]
        }
      ]
    }
  }
};
</script>
