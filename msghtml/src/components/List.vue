<template>
 <div class="index">
   <ul >
     <li v-for="v,i in userList" :key="i">
        <p :style="(setSendData.fd == v.fd)?'background:#999;color:#fff':''" @click="sele(v)">{{v.name}}</p>
    </li>
   </ul>
   {{}}
 </div>
</template>
<script setup>
  defineProps({
    userList:Array,
    setSendData:Object,
  });
  const emits=defineEmits(['setFd'])
  const sele=(obj)=>{
   emits('setFd',obj);
  }
</script>
<style scoped>
.index{
  width:200px;
}
  ul{
    list-style-type:none;
    width:100%;
    padding:0;
    margin:0;
  }
  li{
    border-bottom:1px solid #ccc;
    width:100%;
  }
  p{
    width:100%;
    height:100%;
    padding:5px 0px;
    margin:0;
    cursor:pointer;
  }
</style>