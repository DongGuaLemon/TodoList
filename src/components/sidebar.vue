<template>
<nav id="fixed-sidebar">
  <div class="col-sm-12">
    <!-- <a href="index.html"><img id="home-logo" src="../media/logo-prueba.jpg" alt="Logo de Animanoir"></a>  -->
        <ul style="width:100%">
          <li class="showall"><a  @click="showstatus1">全部</a></li>
          <li class="showend"><a  @click="showstatus2">已完成</a></li>
          <li class="showing"><a  @click="showstatus3">未完成</a></li>
       </ul>
  </div>
</nav>  
</template>

<script>
export default {
  methods:{
    showstatus1(){
      this.$emit('showstatus1')
    },
    showstatus2(){
      this.$emit('showstatus2')
    },
    showstatus3(){
      this.$emit('showstatus3')
    }
  }
}
</script>
<style scoped>
#fixed-sidebar{
  position: fixed;
  max-width: 20%;
  height: 100%;
  background-color: #3498db;
}
ul > li{
 margin:0 auto;
 text-align: center;
 margin-left: -50%;
 list-style: none;
 margin-top:20%; 
}
li:hover{
  color: white;
  cursor: pointer;
}
</style>
