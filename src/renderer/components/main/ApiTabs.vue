<template>
  <el-tabs v-model="editableId" type="card" @tab-remove="removeTab" @tab-click="handleClick">
    <el-tab-pane
        v-for="item in tabsData"
        :label="item.name"
        :key="item.id"
        :name="item.id"
        :closable="true">
      <ApiTable v-model="item.request"></ApiTable>
    </el-tab-pane>
    <el-tab-pane key="add" name="add" :closable="false" label="+"></el-tab-pane>
  </el-tabs>
</template>

<script>
import {uuid} from 'vue-uuid';
import ApiTable from "./ApiTable";

export default {
  name: "ApiTabs",
  components: {ApiTable},
  props: {
    value: {type: Array}
  },
  data() {
    return {
      tabsData: this.value,
      editableId: '',
    }
  },
  created() {
    //console.log(this.value)
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
      if (tab.name === 'add') {
        event.preventDefault()
        this.addTab(this.editableId)
      }
    },
    handleSelect(key, keyPath) {
      console.log(key, keyPath)
    },

    addTab() {
      let id = uuid.v4()
      this.tabsData.push({
        name: 'New Tab',
        id: id,
        content: ''
      });
      this.editableId = id;
    },
    removeTab(targetId) {
      let tabs = this.tabsData;
      let activeId = this.editableId;
      if (activeId === targetId) {
        tabs.forEach((tab, index) => {
          if (tab.id === targetId) {
            let nextTab = tabs[index + 1] || tabs[index - 1];
            if (nextTab) {
              activeId = nextTab.id;
            }
          }
        });
      }

      this.editableId = activeId;
      this.tabsData = tabs.filter(tab => tab.id !== targetId);
    }
  },

}
</script>

<style scoped>

</style>
