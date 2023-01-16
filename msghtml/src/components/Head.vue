<template>
 <div class="index" v-if="isHeadShow">
   <div class="user">用户列表,有{{number}}人在线<br/>选择可聊天</div>
   <div class="info">我是：{{name}}</div>
 </div>
</template>
<script setup>
  defineProps({
    isHeadShow:Boolean,
    name:String,
    number:String,
  });
</script>
<style scoped>
.index{
  border-bottom:3px solid #ccc;
  display:flex;
}
.user{
  background:#409EFF;
  color:#fff;
  width:200px;
  border-right:3px solid #ccc;
}
</style>