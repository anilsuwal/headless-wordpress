<template>
  <div class="blog-section">
    <div class="container">
      <div class="row">
        <div class="col-md-6 col-12" v-for ="proj in projects">
          <div class="single-blog-post">
            <!-- <img :src="proj.yoast_head_json.og_image.url"/> -->
            <p>{{ proj.yoast_head_json.og_image }}</p>
            <a :href="proj.link"><h4 class="blog-title">{{proj.title.rendered}}</h4></a>
            <div class="single-blog-excerpt">{{proj.excerpt.rendered | stripHTML }}</div>
            <a :href="proj.link">Read More</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      projects: []
    }
  },
  created: function(){
    this.$http.get("wp/v2/posts?per_page=100").then(response => {
      for(let project in response.data){
        this.projects.push(response.data[project]);
      }
      console.log(response);
    }, error => { 
      alert(error);
      });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
