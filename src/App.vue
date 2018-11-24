<template>
  <div id="app">
    <input class="addtext" @keyup.enter="Enter" v-model="newlist"/>
    <ul>
      <li v-for="(item,index) in filtertext" :key="index" :class="{finished:item.isFinished}">
       <input type="checkbox" :checked="item.isFinished" @change="endlist(item)"/> 
       <span v-if="!item.isEdit">{{item.label}}</span>
       <input @keyup.enter="update(index,item.label)" v-if="item.isEdit" v-model="item.label">
       <!-- <input @keyup.enter="update(index,$event.target.value )" v-if="item.isEdit" :value="item.label"> -->
       <button @click="edit(index)">編輯</button>
       <button @click="remove(index)">刪除</button>
      </li>
    </ul>
    <div>
      <input type="radio" :checked="showall" @click="show1" :class="{show:showall}" name="show"/><span>全部</span>
      <input type="radio" :checked="showend" @click="show2" :class="{show:showend}" name="show"/><span>已完成</span>
      <input type="radio" :checked="showing" @click="show3" :class="{show:showing}" name="show"/><span>未完成</span>
    </div>
  </div>

</template>

<script>
  export default {
    data () {
      return {
        items: [
          {
            label: 'read books',
            isFinished: false,
            isEdit:false
          },
          {
            label: 'eat dinner',
            isFinished: true,
            isEdit:false
          }
        ],
        newlist:"",
        updatetext:"",
        showall:true,
        showend:false,
        showing:false,
      }
    },
    methods:{
      Enter(){
        this.items.push({label:this.newlist,isFinished:false});
        this.newlist="";
      },
      endlist(item){
        item.isFinished =! item.isFinished;
      },
      remove(index){
        this.items.splice(index,1);
      },
      edit(index){
        this.items[index].isEdit =! this.items[index].isEdit;
      },
      update(index,label){
        this.items[index].label=label;
        this.items[index].isEdit =! this.items[index].isEdit;
      },
      show1(){
        this.showall=true;
        this.showend=false;
        this.showing=false;
      },
      show2(){
        this.showend=true;
        this.showall=false;
        this.showing=false;
      },
      show3(){
        this.showing=true;
        this.showall=false;
        this.showend=false;
      }
    },
    computed:{
      filtertext(){
        if(this.showall==true){
          return this.items;
        }
        if(this.showend==true){
          return this.items.filter(function(item,index,array){
            return item.isFinished==true;
          });
        }
        if(this.showing==true){
          return this.items.filter(function(item,index,array){
            return item.isFinished==false;
          });
        }
      }
    }
  }
</script>
<style>
  #app{
    text-align: center;
    font-size: 30px;
  }
  .finished {
    text-decoration: line-through;
  }
  li{
    list-style: none;
     margin: 10px;
  }
  button{
    margin-left:10px;
  }

</style>