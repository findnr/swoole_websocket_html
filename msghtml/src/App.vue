

<template>
  <div class="box">
     <Login :isLoginShow="isLoginShow" @createWs="createWs"></Login>
     <Head :isHeadShow="isHeadShow" :name="name" :number="number"></Head>
     <Win @setSend="setSend" @send="send" :userList="userList" :infosList="infosList" :setSendData="setSendData"></Win>
  </div>
</template>
<script setup>
  import {ref} from "vue"
  import Login from './components/Login.vue'
  import Head from './components/Head.vue'
  import Win from './components/Win.vue'
  const isLoginShow=ref(true)
  const isHeadShow=ref(false)
  const number=ref(0)
  const name=ref('');
  const userList=ref([]);
  const infosList=ref([])
  const setSendData=ref({});
  
  const setSend=(obj)=>{
      setSendData.value=obj
  }
  const send=(msg)=>{
    let data = {}
    data.path='send/one';
    data.fd=setSendData.value.fd
    Object.assign(data,msg);
    socket.send(JSON.stringify(data))
  }
  let socket = null;
  const createWs=(obj)=>{
    if(socket != null){
      alert('已经登录过，不能重复登录');
      return;
    }
    socket= new WebSocket("wss://swoole.cym504875043.repl.co");
    socket.onopen = function(e) {
      isLoginShow.value=false;
      isHeadShow.value=true
      socket.send(JSON.stringify(obj));
    };
    socket.onmessage = function(event) {
      let data = JSON.parse(event.data)
      control(data);
    };
    socket.onclose = function(event) {
      if (event.wasClean) {
        socket=null;
      } else {
        socket=null;
      }
      midStatus();
    };
    
    socket.onerror = function(error) {
      socket=null;
      midStatus();
    };
  }
  const midStatus=()=>{
    isHeadShow.value=!isHeadShow.value
    isLoginShow.value=!isLoginShow.value
  }
  const control=(obj)=>{
    switch(obj.path){
      case 'login/index':
        loginIndex(obj);
        break;
      case 'list/user':
        listUser(obj);
      case 'msg/list':
        msgList(obj);
        break;
      case 'msg/own':
        msgOwn(obj);
        break;
    }
  }
  const loginIndex=(obj)=>{
    name.value=obj.name;
  }
  const listUser=(obj)=>{
    userList.value=obj.data
    number.value=obj.num
  }
  const msgList=(obj)=>{
    if(obj.title == undefined) return;
    infosList.value.push({type:2,title:obj.title,info:obj.info})
  }
  const msgOwn=(obj)=>{
    if(obj.title == undefined) return;
    infosList.value.push({type:1,title:obj.title,info:obj.info})
  }
</script>
<style scoped>
.box{
  width:1000px;
  height:700px;
  border:3px solid #ccc;
  overflow:hidden;
  border-radius:5px;
}
</style>
