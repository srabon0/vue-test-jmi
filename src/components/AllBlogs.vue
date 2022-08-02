<template>
  <section class="resume-section" :id="blog.id">
    <div class="resume-section-content">
      <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
        <div class="flex-grow-1">
          <h3 class="mb-0">{{ blog.title }} {{ blog.id }}</h3>
          <div class="subheading mb-3">{{ blog.created_by }}</div>
          <p :key="index" v-for="(single, index) in blog.all_blogs">
            {{ blog.all_blogs[index].blog_detail }}
          </p>
        </div>
        <div
          :key="index"
          v-for="(single, index) in blog.all_blogs"
          class="flex-shrink-0"
        >
          <span :key="index" class="text-primary">{{
            blog.all_blogs[index].blog_datetime
          }}</span>
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

          <div class="subheading mb-1">
            <button
              @click="setTemp(blog.id)"
              data-toggle="modal"
              data-target="#exampleModalCenter"
              class="btn btn-sm btn-info"
            >
              New Comment for {{ blog.id }} titled {{ blog.title }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>

  <div
    class="modal fade"
    id="exampleModalCenter"
    tabindex="-1"
    role="dialog"
    aria-labelledby="exampleModalCenterTitle"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLongTitle">Add a Comment</h5>
          <button
            type="button"
            class="close"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit="onSubmit">
            <div class="form-group">
              <label for="exampleFormControlInput1">Name</label>
              <input
                v-model="name"
                type="text"
                class="form-control"
                id="exampleFormControlInput1"
                placeholder="User's name"
              />
            </div>
            <div class="form-group">
              <label for="exampleFormControlTextarea1">Comment</label>
              <textarea
                v-model="comment"
                class="form-control"
                id="exampleFormControlTextarea1"
                rows="3"
              ></textarea>
            </div>

            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-dismiss="modal"
              >
                Close
              </button>
              <input
                type="submit"
                class="btn btn-primary"
                value="Post Comment"
              />
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "AllBlogs",
  props: {
    blog: Object,
  },
  data() {
    return {
      blogId: null,
      name: "",
      comment: "",
    };
  },
  methods: {
    async deleteComment(id) {
      const url = `http://vue-test.gingerbd.com/api/remove-comment/${id}`;
      await axios.get(url).then((response) => console.log(response.data));
      window.location.reload();
    },
    setTemp(id) {
      this.blogId = id;
      console.log(this.blogId);
    },
    async onSubmit(e) {
      e.preventDefault();
      if (!this.name && !this.comment) {
        alert("Please Fill up those field");
        return;
      }
      const commentInfo = {
        name: this.name,
        comment: this.comment,
        date_time: new Date().toJSON().split(".")[0],
      };
      const url = `http://vue-test.gingerbd.com/api/post-comment?blog_id=${this.blogId}&comment=${commentInfo.comment}&comment_datetime=${commentInfo.date_time}&user=${commentInfo.name}`;
      console.log(commentInfo);
      console.log(url);
      await axios.post(url).then((response) => {
        console.log(response);
      });
      (this.name = ""), (this.comment = "");
      window.location.reload();
    },
  },
};
</script>
