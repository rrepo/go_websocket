<template>
  <div>
    <h1>websocket</h1>
    <textarea v-model="textInput"></textarea>
    <button @click="send">send</button>
  </div>
</template>
  
<script setup lang="ts">
const textInput = ref('');
const socket: any = ref()

const send = async () => {

  // let json = JSON.stringify({
  //   "token" : token,
  //   "title": textInput.value,
  // })
  // console.log(token.value)
  socket.value.send(textInput.value);

  textInput.value = ""
}


onMounted(() => {
  // let socket = new WebSocket("ws://localhost:8001/ws");
  socket.value = new WebSocket("ws://localhost:8001/ws");

  socket.value.onopen = function (e: any) {
    console.log(e)
  };

  socket.value.onmessage = function (e: any) {
    console.log(e)
  };

  socket.value.onclose = function (e: any) {
    console.log(e)
    console.log("Close Code = " + e.code);
    console.log("Close Reason = " + e.reason);
  }

})

</script>
  