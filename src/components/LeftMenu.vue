<template>
  <li class="nav-item" :key="blog.id" v-for="blog in blogs">
    <a class="nav-link" :href="'#' + blog.id"> {{ blog.title }} </a>
  </li>
</template>
<script>
export default {
  name: "LeftMenu",
  props: {
    blogs: Array,
  },
};
</script>
