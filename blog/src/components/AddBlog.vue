<template>
  <div id="add-blog">
      <h2>添加博客</h2>
    <form v-if=" !submmited ">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required/>
      <label>博客内容</label>
      <textarea style="resize: none" rows="10" v-model="blog.content">
      </textarea>
      <div id="checkboxs">
        <label>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories">
        <label>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories">
        <label>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories">
        <label>Anglar4.js</label>
        <input type="checkbox" value="Anglar4.js" v-model="blog.categories">
      </div>
      <label>作者</label>
      <select v-model="blog.author">
        <option v-for="author  in authors">{{author}}</option>
      </select>
      <button type="button" @click.prevent="post">添加博客</button>
    </form>

    <div v-if="submmited">
    <h3>博客发布成功</h3>
    </div>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：</p>
      <p>{{blog.content}}</p>
      <p>博客分类</p>
      <ul>
        <li v-for="cate in blog.categories">{{cate}}</li>
      </ul>
      <p>作者:{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'add-blog',
    data () {
      return {
          blog:{
            title:'',
            content:'',
            categories:[],
            author:''
          },
        authors:['A','b','c'],
        submmited:false,

      }
    },
    methods:{
      post(){
        let _this = this /*作用域问题*/
          this.$http.post('http://jsonplaceholder.typicode.com/posts',{
            title:this.blog.title,
            body:this.blog.content,
            userId:1
          }).then(function (data) {
              console.log(data);
              _this.submmited = true;

          })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #add-blog *{
  box-sizing: border-box;
  }
  #add-blog{
    margin: 20px auto;
    max-width: 600px;/*最大宽度*/
    padding: 20px;
  }

  label{
    display: block;/*独占一行*/
    margin: 20px 0 10px;
  }
  input[type='text'],textarea,select{
    display: block;
    width: 100%;
    padding: 8px;
  }
  #checkboxs label{
    display: inline-block;
    margin-top: 0;
  }
  #checkboxs input{
    display: inline-block;
    margin-right: 10px;
  }
  button{
    display: block;
    margin: 20px 0;
    background: crimson;
    color: white;
    border: 0;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
  }
  #preview{
    padding: 10px 20px;
    border: 1px dotted #cccccc;
    margin: 30px 0;
  }
  h3{
    margin-top: 10px;
  }
</style>
