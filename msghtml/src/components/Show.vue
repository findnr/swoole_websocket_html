<template>
 <div class="index" style="width:730px;">
  <ul style="width:100%;">
    <li v-for="v,i in infosList" :key="i" style="padding:10px;width:100%;">
      <div style="" class="box">
        <el-alert style=""
          :title="v.title"
          :type="status[v.type]"
          :description="v.info"
           :closable="false"   
        />
      </div>
    </li>
  </ul>
 </div>
</template>
<script setup>
  defineProps({
    infosList:Array,
  })
  const status=['','success','warning','info']
</script>
<style scoped>
.index{
  padding:10px 0px;
}
ul{
  list-style-type:none;
}
.box{
  
}
</style>