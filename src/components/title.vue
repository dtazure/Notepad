<template>
    <div id="title" ref="title">
           <p>按标题排序</p>
           <p>按创建时间排序</p>
    </div>
</template>
<script>

export default{
   methods:{
       show(){
           this.$refs.title.style.display='block'
       },
        close(){
           this.$refs.title.style.display='none'
       }
   }


}

</script>
<style scoped>

#title{
    display: none;
    width: 140px;
    height: 50px;
    position: absolute;
    left: 63%;
    top: 7%;
    text-align: center;
    z-index: 1;
    background-color: #fff;
}
p{
    height: 25px;
    line-height: 25px;
}
p:hover{
    cursor: pointer;
    background-color: #eee;
}
</style>