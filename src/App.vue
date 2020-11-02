<template>
  <div id="app">
    <div id="BtnBox">
      <Btn color="success" outlined/>
    </div>
  </div>
</template>

<script>
import Btn from './components/Btn.vue'

export default{
  name: 'app',
  components:{
    Btn
  },
  data(){
    return{
      msg: "Hello World!",
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}

#BtnBox{
  height: 100vh;
  display:flex;
  justify-content: center;
  align-items: center;
}
</style>
