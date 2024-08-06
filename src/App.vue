<template>
  <div class="container">
    <el-button type="primary" size="small" v-if="!state.addStatus" @click="state.addStatus = true">新建</el-button>
    <el-input v-if="state.addStatus" size="small" v-model="state.addText" style="width: 150px;margin-right: 10px;" placeholder="又来活了?" />
    <el-button v-if="state.addStatus" size="small" type="primary" @click="save">完成</el-button>
    <el-button v-if="state.addStatus" size="small" type="primary" @click="state.addStatus=false;state.addText=''">取消</el-button>
    <div v-for="(item, index) in state.list" class="che">
      <el-checkbox :label="item.label" :value="item.text" />
      <el-button size="small" type="danger" style="margin-left: auto" @click="del(index)">删除</el-button>
    </div>
  </div>
</template>
<script setup>
import { reactive } from "vue";

const state = reactive({
  list: [
    
  ],
  addStatus: false,
  addText: "",
});
const save = () => {
  state.list.push({
    label: state.addText,
    text: false,
  });
  state.addText = "";
  state.addStatus = false;
  localStorage.setItem("todo", JSON.stringify(state.list));
};
const del=(index)=>{
  state.list.splice(index,1)
  localStorage.setItem("todo", JSON.stringify(state.list));
} 
state.list = JSON.parse(localStorage.getItem("todo")) || [];
</script>

<style lang="scss">
.che {
  display: flex;
  align-items: center;
  font-size: 18px;
}

.el-checkbox__input.is-checked+.el-checkbox__label {
  color: #8d9095 !important;
}

.is-checked .el-checkbox__inner {
  background: #8d9095 !important;
  border-color: #8d9095 !important;
}
</style>
