<template>
 <div class="index">
    <el-input
    v-model="info"
    :rows="3"
    type="textarea"
    placeholder="请输入聊天"
  />
 </div>
  <div>
    <el-button @click="send"  type="primary">发送信息</el-button>
  </div>
</template>
<script setup>
  import {ref} from "vue"
  const info=ref('');
  const emits=defineEmits(['sendData'])
  const send=()=>{
    if(info.value == '') return;
    emits('sendData',{info:info.value})
    info.value=''
  }
</script>
<style scoped>
.index{
  padding:10px;
}
</style>