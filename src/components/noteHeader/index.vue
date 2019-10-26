<template>
  <div class="header">
    <div class="title">vue-notePad</div>
    <div class="build" @click="openBuild">
      新建
      <img src="../../../image/bottomArrow.png" alt />
    </div>
    <div class="all">
      全部
      <div class="total">
        <span class="count">(4)</span>
      </div>
      <img src="../../../image/bottomArrow.png" alt />
    </div>
    <div class="sort">
      按标题排序
      <img src="../../../image/bottomArrow.png" alt />
    </div>
    <input type="text" placeholder="过滤标题、内容、时间戳" />
    <noteBuild ref='build'></noteBuild>
  </div>
</template>
<script>
import noteBuild from '../../components/build'
export default {
  components:{
    noteBuild,
  },
  methods:{
    //父组件调用子组件中的方法，将子组件显示出来
    openBuild(){
      this.$refs.build.show()
    }
  }
}
</script>
<style scoped>
.header {
  width: 1000px;
  height: 50px;
  background-color: #fff;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
  color: #777777;
  font-size: 14px;
  border-bottom: 1px solid #eaea
}
.title{
    height: 50px;
    width: 110px;
    line-height: 50px;
    text-align: center;
    font-size: 18px;
    margin-left: 7px;
    
}
img{
    margin-left: 4px;
}
.build {
  margin-left: 300px;
  width: 90px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  
}
.build:hover,
.all:hover,
.sort:hover {
  background-color: rgb(231, 231, 231);
}
.all {
  
  width: 130px;
  height: 50px;
  display: flex;
  justify-content: flex-start;
  justify-content: center;
  align-items: center;
  vertical-align: middle
}
.count{
    vertical-align: middle
}
.sort {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 130px;
  height: 50px;
}
input {
  width: 180px;
  height: 25px;
  margin-top: 5px;
  margin-left: 12px;
  padding-top: 5px;
  padding-left: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  
}
</style>