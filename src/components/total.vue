<template>
  <div id="total" ref="total" >
    <div class="all" @click="total">
      <span>全部</span>
    </div>
    <div class="work" @click="work">
      <span>工作</span>
    </div>
    <div class="life" @click="life">
      <span>生活</span>
    </div>
    <div class="study" @click="study">
      <span>学习</span>
    </div>
  </div>
</template>
<script>
import bus from '../bus.js'
export default {
  
  mounted(){
     bus.$on('work',work=>{
        this.workList=work

      })
      
      bus.$on('study',study=>{
        this.studyList=study
      })
      bus.$on('life',life=>{
        this.lifeList=life
      })
      bus.$on('total',total=>{
        this.totalList=total
        
      })
  },
  data(){
     return{

       workList:[],
       lifeList:[],
       studyList:[],
       totalList:[]
     }

  },
  methods: {
    show() {
      this.$refs.total.style.display = "block";
    },
    close() {
      this.$refs.total.style.display = "none";
    },
    work() {      
      let filterWork=[]
        for(let i=0;i<this.workList.length;i++){
          if(this.workList[i].style=='工作'){
             filterWork.push(this.workList[i])
             
             bus.$emit('filterWork',filterWork)             
          }
        }
    },
    life(){
      let filterLife=[]
        for(let i=0;i<this.lifeList.length;i++){
          if(this.lifeList[i].style=='生活'){
             filterLife.push(this.lifeList[i])
             bus.$emit('filterLife',filterLife)
          }
        }
    },
    study(){
      let filterStudy=[]
        for(let i=0;i<this.studyList.length;i++){
          if(this.studyList[i].style=='学习'){
             filterStudy.push(this.studyList[i])
             
             bus.$emit('filterStudy',filterStudy)
          }
        }
    },
    total(){
     let filterTotal=this.totalList
       bus.$emit('filterTotal',filterTotal)
    },
  }
};
</script>
<style scoped>
#total {
  display: none;
  width: 120px;
  height: 130px;
  position: absolute;
  left: 65%;
  top: 7%;
  border: 1px solid rgb(229, 229, 229);
  z-index: 1;
  background-color: #fff;
}
.all,
.work,
.life,
.study {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.all:hover,
.work:hover,
.life:hover,
.study:hover {
  cursor: pointer;
  background-color: #eee;
}
.all {
  height: 40px;
  border-bottom: 1px solid rgb(229, 229, 229);
}
.work,
.life,
.study {
  margin-top: 8px;
}
</style>