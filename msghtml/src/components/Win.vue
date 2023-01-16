<template>
 <div class='index'>
    <div class='left'>
      <el-scrollbar height="650px">
        <List :setSendData="setSendData" :userList="userList" @setFd="setFd"></List>
      </el-scrollbar>
    </div>
   <div class='right'>
     <div class="show">
        <el-scrollbar height="500px">
          <Show :infosList="infosList"></Show>
        </el-scrollbar>
     </div>
     <div class="send">
        <Send @sendData="sendData"></Send>
     </div>
   </div>
 </div>
</template>
<script setup>
  import {ref,reactive} from "vue"
  import List from './List.vue'
  import Show from './Show.vue'
  import Send from './Send.vue'
  defineProps({
    userList:Array,
    infosList:Array,
    setSendData:Object,
  })
  const emits=defineEmits(['setSend','send'])
  const setFd=(obj)=>{
    emits('setSend',obj)
  }
  const sendData=(msg)=>{
    emits('send',msg);
  }
</script>
<style scoped>
.index{
  display:flex;
}
.left{
  border-right:3px solid #ccc;
  width:200px;
}
.right{
  flex:1;
}
.send{
  height:150px;
  border-top:3px solid #ccc;
}
</style>