<template>
<div class="bgc">
  <div id="app">
    <noteHeader></noteHeader>
    <noteBody></noteBody>
   
    <router-view/>
  </div>
  </div>
</template>

<script>
import noteHeader from './components/noteHeader/index'
import noteBody from './components/noteBody'




export default {
  components:{
    noteHeader,
    noteBody,
    
   
  },
  name: 'App'
}
</script>

<style scoped>
body{
    background: url('../image/pixels.png');

}
#app{
  width: 1000px;
  height: 700px;
  background-color: #fff;
  border: 1px solid rgb(189,189,189);
  margin: 0 auto;
  position: relative;
   background:url('../image/dd.jpg') 

}
.bgc{
  width: 100%;
  background: url('../image/pixels.png')
}
</style>
