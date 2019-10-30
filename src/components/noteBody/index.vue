<template>
  <div id="allList">
    <div class="list" ref="note" v-for="(item,index) in items" :key="index" track-by="$index">
      <div class="list_header">
        <div class="title">{{item.title}}</div>
        <img class="after" src="../../../image/revise1.png" @click="revise(index)">
        <img class="after" src="../../../image/delete1.png" @click="delate(index)">
      </div>
      <div class="info">
        <span>{{item.time}}</span>
        <span>分类:{{item.style}}</span>
      </div>
      <div class="content">{{item.content}}</div>
    </div>
    <revise ref="revise" :list='list'></revise>
  </div>
</template>
<script>
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
import bus from "../../bus.js";
import revise from './revise'
export default {
  mounted() {
    bus.$on("build", data => {
      this.time = `${date}-${day},${hour}:${minutes}`;
      this.title = data.title;
      this.content = data.content;
      this.style = data.value;
    });
    bus.$on("build", this.build);
  },
  components:{
    revise
  },
  data() {
    return {
      title: "",
      time: "",
      content: "",
      style: "",
      items: [
        {
          title: "购物",
          time: "10-07, 00:00",
          content: "蓝月亮袋装洗衣液",
          style: "2"
        }
      ],
      list:{
          title:'',
          time:'',
          content:'',
          style:''
      }
    };
  },
  methods: {
    build() {
      this.items.push({
        title: this.title,
        time: this.time,
        style: this.style,
        content: this.content
      
      });
    },
    revise(index){
      this.$refs.revise.show()
      this.list.title=this.items[index].title
      this.list.content=this.items[index].content
      this.list.style=this.items[index].style
    },
    delate(index){      
       this.items.splice(index,1)
    }
  }
};
</script>
<style scoped>
#allList {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap
 
}
.list {
  width: 215px;
  height: 290px;
  padding: 9px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  border: 1px solid rgb(189, 189, 189);
  margin-left: 12px;
  margin-top: 10px
 
 
}
.list_header {
  width: 240px;
  height: 24px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-size: 14px;
  position: relative;
}
.title {
  max-width: 170px;
  height: 22px;
  border-bottom: 1px solid rgb(189, 189, 189);
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
img:nth-child(2) {
  position: absolute;
  left: 175px;
}
img:nth-child(3) {
  position: absolute;
  left: 200px;
}
img:hover {
  cursor: pointer;
}

.info {
  font-size: 12px;
  color: #757575;
  font-weight: 300;
  margin-top: 5px;
}
.info span:nth-child(3) {
  margin-left: 50px;
}
.content {
  margin-top: 10px;
  font-size: 15px;
}
</style>
