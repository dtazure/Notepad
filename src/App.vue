<template>
  <div id="app">
    <noteHeader></noteHeader>
    <noteBody></noteBody>
   
    <router-view/>
  </div>
</template>

<script>
import noteHeader from './components/noteHeader/index'
import noteBody from './components/noteBody'


export default {
  components:{
    noteHeader,
    noteBody
   
  },
  name: 'App'
}
</script>

<style scoped>
#app{
  width: 1000px;
  height: 700px;
  background-color: #fff;
  border: 1px solid #333;
  margin: 0 auto
}
</style>
