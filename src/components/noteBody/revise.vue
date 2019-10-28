<template>
  <div id="build" ref="build">
    <div class="header">
      <input type="text" placeholder="标题"  v-model="title">
      <select v-model="value">
        <option :value="1">工作</option>
        <option :value="2">学习</option>
        <option :value="3">生活</option>
      </select>
      <img @mouseover="over1" src="../../image/save.png" alt ref="beforeImg">
      <img
        @mouseleave="leave1"
        @click="build"
        class="after"
        src="../../image/save1.png"
        alt
        ref="afterImg"
      >
      <img @mouseover="over2" src="../../image/cancel.png" alt ref="beforeImg2">
      <img
        @mouseleave="leave2"
        @click="closeBuild"
        class="after"
        src="../../image/cancel1.png"
        alt
        ref="afterImg2"
      >
    </div>
    <textarea placeholder="内容.." v-model="content"></textarea>
  </div>
</template>
<script>
import bus from '../bus.js'
export default {
  data(){
    return{
          title:'',
          type:'',
          content:'',
          value:'1'
    }
  },
  methods: {
    //保存和取消按钮的样式改变
    over1() {
      this.$refs.beforeImg.style.display = "none";
      this.$refs.afterImg.style.display = "block";
    },
    over2() {
      this.$refs.beforeImg2.style.display = "none";
      this.$refs.afterImg2.style.display = "block";
    },
    leave1() {
      this.$refs.beforeImg.style.display = "block";
      this.$refs.afterImg.style.display = "none";
    },
    leave2() {
      this.$refs.beforeImg2.style.display = "block";
      this.$refs.afterImg2.style.display = "none";
    },
    //build组件的显示与隐藏
    show() {
      this.$refs.build.style.display = "block";
    },
    closeBuild() {
      this.$refs.build.style.display = "none";
      
    },
    build(){
      const data ={
        title : this.title,
        content : this.content,
        value:this.value
      }
      
        bus.$emit('build',data)
        this.title=''
        this.content=''
        this.value='1'
    }
  }
};
</script>
<style scoped>
#build {
  display: none;
  width: 280px;
  height: 330px;
  position: absolute;
  left: 45%;
  top: 30%;
  background-color: #eeee;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  z-index: 1
}
.header {
  margin-left: 12px;
  margin-top: 9px;
  width: 260px;
  height: 35px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
input {
  width: 120px;
  height: 30px;
  padding-left: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
select {
  margin-left: 15px;
  height: 30px;
  padding-left: 4px;
  border-radius: 5px;
}
select:hover {
  cursor: pointer;
  background-color: rgb(230, 230, 230);
}
option {
  background-color: #fff;
}
option:hover {
  background-color: rgb(230, 230, 230);
}
img {
  margin-left: 13px;
}
img:hover {
  cursor: pointer;
}
.after {
  display: none;
}
textarea {
  margin-left: 14px;
  margin-top: 8px;
  width: 250px;
  height: 260px;
  resize: none;
  border-radius: 5px;
  padding-left: 6px;
  padding-top: 5px;
}
</style>