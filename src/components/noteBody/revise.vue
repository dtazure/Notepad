<template>
  <div id="build" ref="build">
    <div class="header">
      <input type="text" placeholder="标题"  v-model="title">
       <select v-model="value">
        <option :value="style[0].name">工作</option>
        <option :value="style[1].name">生活</option>
        <option :value="style[2].name">学习</option>
      </select>
      <img @mouseover="over1" src="../../../image/save.png" alt ref="beforeImg">
      <img
        @mouseleave="leave1"
        class="after"
        @click="save"
        src="../../../image/save1.png"
        ref="afterImg"
      >
      <img @mouseover="over2" src="../../../image/cancel.png" alt ref="beforeImg2">
      <img
        @mouseleave="leave2"
        @click="closeBuild"
        class="after"
        src="../../../image/cancel1.png"
        ref="afterImg2"
      >
    </div>
    <textarea placeholder="内容.." v-model="content"></textarea>
  </div>
</template>
<script>
import bus from "../../bus.js";
var now = new Date();
var date = now.getMonth() + 1;
var day = now.getDate();
var hour = now.getHours();
var minutes = now.getMinutes();
if (day < 10) {
  day = "0" + day;
}
if (date < 10) {
  date = "0" + date;
}
if (hour < 10) {
  hour = "0" + hour;
}
if (minutes < 10) {
  minutes = "0" + minutes;
}

export default {
  props:{
    list:{
  
    }
  },
  data(){
    return{
          title:'',
          type:'',
          content:'',
          value:'',
          index:'',
          style: [
        {
          name: "工作"
        },
        {
          name: "生活"
        },
        {
          name: "学习"
        }
      ]
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
    show(index) {
       this.content=this.list.content
      this.title=this.list.title
      this.time=this.list.time
      this.value=this.list.style
        this.index=index 
                     
      
      this.$refs.build.style.display = "block";
    },
    closeBuild() {
      bus.$emit('closePop')
      this.$refs.build.style.display = "none";
      
    },
    save(){
      
        const data = {
          index:this.index,
          title:this.title,
          time:`${date}-${day},${hour}:${minutes}`,
          style:this.value,
          content:this.content
        }
        bus.$emit('save',data)
        bus.$emit('closePop')
        this.$refs.build.style.display = "none";

      


    },
    showDetail(){
      
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
  z-index: 20
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