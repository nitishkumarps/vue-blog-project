<template>
  <div v-theme:column="" id="show-blogs">
   <h1>All blog Articles</h1>
   <input type="text" v-model="search" placeholder="search blogs" />
 <div v-for="(blog,index) in filteredBlogs" class="single-blog" :key="index">
  <router-link v-bind:to="'/blog/'+blog.id"> <h2>{{blog.title | to-uppercase}}</h2></router-link>
  <article>{{blog.content | snippet}}</article>
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
   this.$http.get("https://vue-blog-project-9dc82-default-rtdb.firebaseio.com/posts.json").then(response=>{
     let responseData=response.data;
     let temp=[];
     for(let i in responseData)
     {
       responseData[i].id=i;
       temp.push(responseData[i]);
     }
     this.blogs=temp;
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
