<template>
  <div>
    B11111组件
    <div class="box" :class="{con:index==1}" @click="conder(1)">12345</div>
    <div class="box" :class="{con:index==2}" @click="conder(2)">12345</div>
    <div class="box" :class="{con:index==3}" @click="conder(3)">12345</div>
    <div class="box" :class="{con:index==4}" @click="conder(4)">12345</div>
    <!-- <div class="box" :class="showform?'con':'' " @click="conder(2)">12345</div> -->
  </div>
</template>
<script>
export default {
  // 适用于路由组件没有缓存
  // mounted () {
  //   console.log('b1 mounted()')
  //   this.timeId = setInterval(() => {
  //     console.log('做些事件...111')
  //   }, 1000)
  // },
  // // 卸载后干掉定时器
  // beforeDestroy() {
  //   clearInterval(this.timeId)
  // },

  // // // 在每次准备进入前
  beforeRouteEnter(to, from, next) {
    next(component => {
      component.intervalId = setInterval(() => {
        console.log("做些事件...");
      }, 1000);
    });
  },

  // // 在当前组件离开前调用, 可以访问this
  beforeRouteLeave(to, from, next) {
    clearInterval(this.intervalId);

    next();
  },
  data(){
    return {
      index:null,
      showform: false
    }
  },
  methods: {
    conder(index) {
      this.index =index
      this.showform = true;
    }
  }
};
</script>
<style lang='css'>
 .box{
   margin-bottom: 20px;
 }
.con{
width:100px;
height:100px;
background:yellow;
transform: scale(1.2);
transition:all 1s;

}
</style>