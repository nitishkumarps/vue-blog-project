<template>
  <div id="add-blog">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted" >
     <label>Blog Title</label>
     <input type="text" required v-model.lazy="blog.title" />
     <label>Blog Content</label>
     <textarea v-model.lazy="blog.content"></textarea>
     <div id="checkboxes">
    <label>Hidden Leaf Village</label>
    <input type="checkbox" value="leaf" v-model="blog.categories" />
    <label>Sand Village</label>
    <input type="checkbox" value="sand" v-model="blog.categories" />
    <label>Sound Village</label>
    <input type="checkbox" value="sound" v-model="blog.categories" />
    </div>
    <label>Author:</label>
    <select v-model="blog.author">
      <option value="">Select</option>
      <option v-for="(author,index) in authors" :key="index">{{author}}</option>
    </select>
    <button v-on:click.prevent="post">Add Blog</button>
    </form>
    <div v-if="submitted">
      <h3>Thanks for Submitting the form</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>BLog Title: {{blog.title}}</p>
      <p>Blog content: </p>
      <p>{{blog.content}}</p>
      <p>Blog Categories</p>
      <ul>
        <li v-for="(cat,index) in blog.categories" :key="index" >{{cat}}</li>
      </ul>
      <p>Author: {{blog.author}}</p>
    </div>
  </div> 
</template>
<script>

export default {
  
  data () {
    return {
      blog:{
      title:"",
      content:"",
      categories:[],
      author:""
      },
      authors:["Naruto","Sauske","Lee"],
      submitted:false,
      
    } 
  },
  methods:{
    post:function(){
      this.$http.post("https://vue-blog-project-9dc82-default-rtdb.firebaseio.com/posts.json",this.blog).then(function(data){
        console.log(data);
        this.submitted=true;
      })
    }
  }
  
}
</script>

<style >
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#checkboxes input {
display: inline block;
margin-right: 20px;
}
#checkboxes label {
   display: inline-block;
}

</style>
