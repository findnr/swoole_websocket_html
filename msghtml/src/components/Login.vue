<template>
 <div v-if="isLoginShow" class='index'>
   <el-button @click="open" type="success">登录</el-button>
   <el-dialog v-model="isBox" title="Warning" width="30%" center>
    <span>
     请输入名称： <el-input v-model="name" type="text" placeholder="请输入名称" />
    </span>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="isBox= false">关闭</el-button>
        <el-button type="primary" @click="submit">
          提交
        </el-button>
      </span>
    </template>
  </el-dialog>
 </div>
</template>
<script setup>
  import {ref} from "vue"
  import { ElMessage, ElMessageBox } from 'element-plus'
  defineProps({
    isLoginShow:Boolean,
  });
  const emits=defineEmits(['createWs']);
  const isBox=ref(false)
  const name=ref('')
  const open=()=>{
    isBox.value = true
  }
  const submit=()=>{
    if(name.value == ''){
      ElMessage('用户名不能为空');return;
    }
    emits('createWs',{path:'login/index',name:name.value})
    
  }
</script>



<style scoped>
.index{
  padding:5px 0px;
  border-bottom:3px solid #ccc;
}
</style>