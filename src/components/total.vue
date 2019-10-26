<template>
  <div id="total" ref="total">
    <div class="all">
      <span>全部</span>
      <span>14</span>
    </div>
    <div class="work">
      <span>工作</span>
      <span>8</span>
    </div>
    <div class="life">
      <span >生活</span>
      <span>3</span>
    </div>
    <div class="study">
      <span >学习</span>
      <span>3</span>
    </div>
  </div>
</template>
<script>
export default {
    methods:{
        show(){
              this.$refs.total.style.display='block'
         },
         close(){
              this.$refs.total.style.display='none'
         },
    }
}
</script>
<style scoped>
#total {
display: none;
  width: 160px;
  height: 130px;
  position: absolute;
  left: 48%;
  top: 7%;
  border:1px solid rgb(229,229,229)
}
.all,.work,.life,.study {
 
  display: flex;
  justify-content:space-around;
  align-items: center;
 
}
.all:hover,.work:hover,.life:hover,.study:hover{
    cursor: pointer;
    background-color: #eee;
}
.all{
 height: 40px;
  border-bottom: 1px solid rgb(229,229,229)
}
.work,.life,.study{
    margin-top: 8px;

}
</style>