<template>
  <nav
    class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top"
    id="sideNav"
  >
    <a class="navbar-brand js-scroll-trigger" href="#page-top">
      <span class="d-none d-lg-block"
        ><img
          class="img-fluid img-profile mx-auto mb-2"
          src="assets/img/JERPLOGO2.png"
          alt=""
          style="border: none"
      /></span>
    </a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link js-scroll-trigger" href="#about">Instructions</a>
        </li>
        <li class="nav-item">
          <a class="nav-link js-scroll-trigger" href="#">BLOG</a>
        </li>
        <li class="nav-item">
          <a class="nav-link js-scroll-trigger" href="#"><hr /></a>
        </li>
        <li class="nav-item">
          <a class="nav-link js-scroll-trigger" href="#experience"
            >Example Blog</a
          >
        </li>
        <LeftMenu :blogs="blogs" />
        <!-- vue component -->
        <!-- <li class="nav-item" :key="blog.id" v-for="blog in blogs">
          <a :href="'#' + blog.id"> {{ blog.title }} </a>
        </li> -->
      </ul>
    </div>
  </nav>
</template>
<script>
import LeftMenu from "./components/LeftMenu.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    LeftMenu,
  },
  data() {
    return {
      blogs: null,
      allBlogs: this.getAllblogs(),
    };
  },
  created() {
    axios
      .get("http://vue-test.gingerbd.com/api/blogs")
      .then((response) => {
        this.blogs = response.data.blogs;
        console.log(this.blogs);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    async getAllblogs() {
      var vas = await axios.get("http://vue-test.gingerbd.com/api/all-blogs");
      this.allBlogs = vas.data;
    },
  },
};
</script>
