<template>
  <div class="hello">
  	<input v-model="newItem" v-on:keyup.enter="addNew">
    <h1>{{ title }}</h1>
 <ul>
  <li v-for="item in items" v-bind:class="{finished:item.isFinshed}" v-on:click="toggleFinish(item)">
    {{item.label}}
  </li>
  </ul> </div>

</template>

<script>
  import Store from './store'
  export default {
  data () {
    return {
     title: 'this is a to dolist',
     items:[
     ]
    /*, liclass:'thisisliclass',
     liclass2:'thisisliclass2'*/
,newItem:''
    }
  },
  watch:{
    items:{
handler:function(items){
  Store.save(items)
},
deep:true
    }
  },
  methods:{
  	toggleFinish:function(item){
  		item.isFinshed=!item.isFinshed
  	},
  	addNew:function(){
  		this.items.push({
  			label:this.newItem,
  			isFinshed:false
  		})
  		this.newItem=''
  	}
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.finished{
  text-decoration:underline;
}
ul {
  list-style-type: none;
  padding:0px;
}
li {
  
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
