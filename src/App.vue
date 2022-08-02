<template>
  <div>
    <nav
      class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top"
      id="sideNav"
    >
      <a class="navbar-brand js-scroll-trigger" href="#page-top">
        <span class="d-none d-lg-block"
          ><img
            class="img-fluid img-profile mx-auto mb-2"
            src="./assets/JERPLOGO2.png"
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
    <div class="container-fluid p-0">
      <!-- About-->
      <section class="resume-section" id="about">
        <div class="resume-section-content">
          <h1 class="mb-0">
            Vue Test
            <span class="text-primary">MononSoft</span>
          </h1>
          <div class="subheading mt-3">Instructions:</div>
          <div class="lead mb-5">
            <ul class="fa-ul mb-0">
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Populate Left Menu under BLOG
              </li>
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Get Detail of Selected Blog and Comments and view in main
                content area
              </li>
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Make a Modal for Comment on click New Comment Button
              </li>
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Receive Commenter Name, Comment and current date time for from
                Comment Submit
              </li>
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Create or remove new comment and display
              </li>
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                Maintain SPA while develop
              </li>
            </ul>
            <div class="subheading mt-5">API's:</div>
            <div class="lead mt-3">
              <ul class="fa-ul mb-0">
                <li>
                  <span class="fa-li"><i class="fas fa-check"></i></span>
                  ALL-BLOGS [get] ["http://vue-test.gingerbd.com/api/all-blogs"]
                </li>
                <li>
                  <span class="fa-li"><i class="fas fa-check"></i></span>
                  LEFT-MENU [get] ["http://vue-test.gingerbd.com/api/blogs"]
                </li>
                <li>
                  <span class="fa-li"><i class="fas fa-check"></i></span>
                  VIEW-BLOG [get]
                  ["http://vue-test.gingerbd.com/api/view-blog/id"]
                </li>
                <li>
                  <span class="fa-li"><i class="fas fa-check"></i></span>
                  SAVE COMMENT [post]
                  ["http://vue-test.gingerbd.com/api/post-comment?blog_id=blog_id&comment=comment&comment_datetime=now()&user=user"]
                </li>
                <li>
                  <span class="fa-li"><i class="fas fa-check"></i></span>
                  DELETE COMMENT [get]
                  ["http://vue-test.gingerbd.com/api/remove-comment/id"]
                </li>
              </ul>
            </div>
          </div>
        </div>
      </section>
      <hr class="m-0" />
      <div :key="blog.id" v-for="blog in allBlogs">
        <AllBlogs :blog="blog" />
      </div>
      <!-- Experience-->
    </div>
  </div>
</template>
<script>
import LeftMenu from "./components/LeftMenu.vue";
import AllBlogs from "./components/AllBlogs.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    LeftMenu,
    AllBlogs,
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
      console.log(this.allBlogs);
    },
  },
};
</script>
