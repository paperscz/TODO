<template>
  <div class="list">
    <h2><span class="title">TODO</span>列表</h2>
    <div class="search">
      <input type="text" v-model="search" placeholder="请输入搜索内容">
    </div>
    <div class="list-item" v-for="item in filterItem">
      <router-link v-bind:to="'/list/' + item.id">
        <p>{{item.name}}</p>
      </router-link>
    </div>
    <div class="addList">
      <router-link v-bind:to="'/add'">
        <button>添加计划</button>
      </router-link>
    </div>
    <!-- <div class="button">
      <button @click.prevent="upPage">上一页</button>
      <button @click.prevent="nextPage">下一页</button>
    </div> -->
  </div>
  
</template>

<script>
export default {
  name: 'index',
  data () {
    return {
      items : [],
      search : '',
      pageFlag : false
    }
  },
  created () {
    this.$http.get('https://my-first-vue.firebaseio.com/add.json')
    .then((data) => {
      console.log(data.json())
      return data.json()
    })
    .then(data => {
      let arr = []
      for(let key in data){
        //console.log(key)
        //console.log(data[key])
        data[key].id = key
        arr.push(data[key])
      }
      this.items = arr
      if(this.items.length > 10){
        this.pageFlag = true;
        this.items.slice(0, 10)
      }
    })
  },
  methods : {
    upPage : () =>{


    },
    nextPage : () => {

    }
  },
  computed : {
    //filterItem : () => this.items.filter(item => item.name.match(this.search))
    filterItem : function(){
      return this.items.filter((item) =>{
        return item.name.match(this.search);
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list{
  box-sizing: border-box;
  max-width: 800px;
  min-height: 700px;
  margin: 0 auto;
  padding-top: 10px;
  border-radius: 10px;
  background-color: rgba(83,113,134,.7);
  box-shadow: 10px 10px 5px #1F2C52;
}
input{
  width: 77%;
  height: 30px;
  padding: 0 10px;
}
.list-item{
  width: 79%;
  background-color: rgba(243,243,243,.8);
  margin: 10px auto;
  min-height: 40px;
  line-height: 40px;
  padding-left: 10px;
  border-radius: 5px;
}
.list-item > p{
 
  line-height: 40px;
  text-indent: 2em;
}
.search{
  text-align: center;
}
h2{
  color: #f9f9f9;
  font-size: 30px;
}
h2,h3{
  text-align: center;
}
.title{
  text-shadow: 3px 3px 3px #FF0000;
}
.button{
  /*margin: 0 auto;*/
  text-align: center;
}
a{
  text-decoration: none;
  color: rgba(0,102,255,.49);
}
button{
  border: 0;
  background-color: #3A97BB;
  width: 80px;
  height: 30px;
  border-radius: 4px;
  font-size: 14px;
  color: #fff;
}
button:hover{
  background-color: #D06B66;
}
.addList{
  margin-top: 10px;
  text-align: center;
}

</style>
