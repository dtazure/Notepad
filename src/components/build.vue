<template>
  <div id="build" ref="build">
    <div class="header">
      <input type="text" placeholder="标题" v-model="title">
      <select v-model="value">
        <option :value="style[0].name">工作</option>
        <option :value="style[1].name">生活</option>
        <option :value="style[2].name">学习</option>
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
import bus from "../bus.js";
export default {
  created() {
    //如果没有这句代码，select中初始化会是空白的，默认选中就无法实现
    this.value = this.style[0].name;
  },
  data() {
    return {
      title: "",
      type: "",
      content: "",
      value: "",
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
    };
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
      bus.$emit('closePop')
      this.title = "";
      this.content = "";
      this.value = this.style[0].name;
      this.$refs.build.style.display = "none";
    },
    build() {
      bus.$emit('closePop')
      if(this.title==''){
         alert('请输入标题~')
      }else if(this.content==''){
        alert('请输入内容~')
      }else{
        const data = {
        title: this.title,
        content: this.content,
        value: this.value
      };
      bus.$emit("build", data);
      this.title = "";
      this.content = "";
      this.value = this.style[0].name;
      }
      this.$refs.build.style.display='none'
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
  z-index: 20;
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