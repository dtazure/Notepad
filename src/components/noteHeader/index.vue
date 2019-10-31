<template>
  <div class="header">
        <div class="popContainer" ref="pop"></div>

    <div class="title">vue-notePad</div>
    <div class="build" @click="openBuild">
      新建
      <img src="../../../image/bottomArrow.png" alt />
    </div>
    <div class="all" @click="switchTotal">
      全部
      <div class="total">
        <span class="count">(4)</span>
      </div>
      <img src="../../../image/bottomArrow.png" alt />
    </div>
    <!-- <div class="sort" @click="switchTitle">
      按标题排序
      <img src="../../../image/bottomArrow.png" alt />
    </div> -->
    <input type="text" placeholder="过滤标题"  v-model="queryString" @keyup="filterBy(queryString)">
    <noteBuild ref="build" ></noteBuild>
    <total ref="total"></total>
    <noteTitle ref="title"></noteTitle>
  </div>
</template>
<script>
import noteBuild from "../../components/build";
import total from "../../components/total";
import noteTitle from "../../components/title";
import bus from '../../bus.js'


let flag = 1;
export default {
  mounted(){
     bus.$on('tansform',data=>{
            this.items=data  
     });
     bus.$on('closePop',this.closePop)
     bus.$on('showPop',this.showPop)
     
  },
  components: {
    noteBuild,
    total,
    noteTitle,

  },
  data(){
    return{
        queryString:'',
        items:[],
        memosFiltered:[]
    }
  },
  methods: {
    closePop(){
      this.$refs.pop.style.display='none'
    },
    filterBy(queryString){
        if(queryString==''){
           bus.$emit('filter',this.items)
        }
        if(queryString!==''){
          for(let i=0;i<this.items.length;i++){
            if (this.items[i].title.indexOf(queryString) !== -1) {
              const data=[
                {
                  title:this.items[i].title,
                  time:this.items[i].time,
                  content:this.items[i].content,
                  style:this.items[i].style
                }
              ]
                 bus.$emit('filter',data) 
      }
          }
        }
    },
    showPop(){
       this.$refs.pop.style.display='block'
    },
    //父组件调用子组件中的方法，将子组件显示出来
    openBuild() {
      this.$refs.pop.style.display='block'
      this.$refs.build.show();
    },
    //全部子组件的显隐
    switchTotal() {
      if (flag) {
        flag = 0;
        this.$refs.total.show();
      } else {
        flag = 1;
        this.$refs.total.close();
      }
    },
    //按标题排序子组件的显隐
    switchTitle(){
      if (flag) {
        flag = 0;
        this.$refs.title.show();
      } else {
        flag = 1;
        this.$refs.title.close();
      }
    }
  }
};
</script>
<style scoped>
.popContainer{
  display:none;
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba(0,0,0,0.3);
  z-index: 10;
}
.header {
  width: 1000px;
  height: 50px;
  background-color: #fff;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #777777;
  font-size: 14px;
  border-bottom: 1px solid #eaea;

}
.title {
  height: 50px;
  width: 110px;
  line-height: 50px;
  text-align: center;
  font-size: 18px;
  margin-left: 7px;
}
img {
  margin-left: 4px;
}
.build {
  margin-left: 440px;
  width: 90px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.build:hover,
.all:hover,
.sort:hover {
  cursor: pointer;
  background-color: rgb(231, 231, 231);
}
.all {
  width: 130px;
  height: 50px;
  display: flex;
  justify-content: flex-start;
  justify-content: center;
  align-items: center;
  vertical-align: middle;
}
.count {
  vertical-align: middle;
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