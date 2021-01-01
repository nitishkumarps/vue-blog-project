<template>
  <div v-theme:column="" id="show-blogs">
   <h1>List Blog Titles</h1>
   <input type="text" v-model="search" placeholder="search blogs" />
 <div v-for="(blog,index) in filteredBlogs" class="single-blog" :key="index">
  <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
  
 </div>
  
  </div>
</template>
<script>


import searchMixin from "../mixins/searchMixin";
export default {
   
  data () {
    return {
     blogs:[],
     search:"",
    } 
  },
  methods:{

  },
  created(){
   this.$http.get("https://jsonplaceholder.typicode.com/posts").then(response=>{
   this.blogs= response.data.slice(0,10);
   })
  },
  computed:{
   
  },
  //Local Filter registration
  filters:{
   "to-uppercase":(value)=>{
    return value.toUpperCase();
   },
   // another type of defining filter
   snippet(value){
    return value.slice(0, 100) + "..."; // returning 100 characters
   }
  },
  directives:{
   "rainbow":{
    bind(el,binding,vnode){
     el.style.color = "#" + Math.random().toString().slice(2, 8);
    }
   }
  },
  mixins:[searchMixin]

  
}
</script>

<style >
#show-blogs{
 max-width: 800px;
 margin:0 auto;
}
.single-blog{
 padding:20px;
 margin :20px 0px;
 box-sizing: border-box;
 background:#eee ;
}

</style>
