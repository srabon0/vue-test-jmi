<template>
  <section class="resume-section" id="blog.id">
    <div class="resume-section-content">
      <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
        <div class="flex-grow-1">
          <h3 class="mb-0">{{ blog.title }}</h3>
          <div class="subheading mb-3">{{ blog.created_by }}</div>
          <p :key="index" v-for="(single, index) in blog.all_blogs">
            {{ blog.all_blogs[index].blog_detail }}
          </p>
        </div>
        <div class="flex-shrink-0">
          <span class="text-primary">11 March 2013 : 10am</span>
        </div>
      </div>
      <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
        <div class="flex-grow-1">
          <h5 class="mb-0">
            Blog Comment
            <hr />
          </h5>
          <div class="subheading mb-1" style="font-size: 11pt">
            <i class="fa fa-user"></i> Commenter 1
            <div class="float-right">
              <i class="fa fa-clock"></i> 2021-03-23 10.05 pm
            </div>
          </div>
          <p>Comment 1</p>
          <div class="subheading mb-1" style="font-size: 11pt">
            <i class="fa fa-user"></i> Commenter 2
            <div class="float-right">
              <i class="fa fa-clock"></i> 2021-03-23 10.05 pm
            </div>
          </div>
          <p>Comment 2</p>
          <div class="subheading mb-1">
            <button class="btn btn-sm btn-info">New Comment</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "AllBlogs",
  props: {
    blog: Object,
  },
};
</script>
