<template>

  <div id="allList"  >
    <div class="list" ref="note" v-for="item in items" :key="item">
      <div class="list_header">
        <div class="title">13213112321323123132132132132112321312321321</div>
        <img @mouseover="over1" src="../../../image/revise.png" alt ref="beforeImg">
        <img @mouseleave="leave1" class="after" src="../../../image/revise1.png" alt ref="afterImg" style="display:none">
        <img @mouseover="over2" src="../../../image/delete.png" alt ref="beforeImg2">
        <img
          @mouseleave="leave2"
          class="after"
          src="../../../image/delete1.png"
          alt
          ref="afterImg2"
          style="display:none"
        >
      </div>
      <div class="info">
        <span>10-26</span>,
        <span>15:19</span>
        <span>分类:工作</span>
      </div>
      <div class="content">32132</div>
    </div>
  </div>
 
</template>
<script>

import bus from '../../bus.js'
export default {
  mounted(){
    bus.$on('build',this.build)
  },
  data() {
    return {
      items: ['this.$refs.note']
    };
  },
  methods: {
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
    build(){
        this.items.push('this.$refs.note')
    }
    
  }
};
</script>
<style scoped>
#allList {
  display: flex;
  justify-content: flex-start;
}
.list {
  width: 260px;
  height: 340px;
  padding: 9px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.list_header {
  width: 260px;
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
img:nth-child(2),
img:nth-child(3) {
  position: absolute;
  left: 175px;
}
img:nth-child(4),
img:nth-child(5) {
  position: absolute;
  left: 200px;
}

img:hover {
  cursor: pointer;
}
.after {
  display: none;
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
