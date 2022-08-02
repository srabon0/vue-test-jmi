<template>
  <section class="resume-section" :id="blog.id">
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
          <div
            :key="comment.id"
            v-for="comment in blog.all_comments"
            class="subheading mb-1"
            style="font-size: 11pt"
          >
            <i class="fa fa-user"></i> {{ comment.user }}
            <div class="float-right">
              <i class="fa fa-clock"></i> {{ comment.comment_datetime }}
            </div>
            <p>
              {{ comment.comment }}
              <span
                style="cursor: pointer"
                data-toggle="tooltip"
                data-placement="right"
                title="delete this comment"
                @click="deleteComment(comment.id)"
                class="mx-5"
              >
                <i class="fa fa-trash"></i>
              </span>
            </p>
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
