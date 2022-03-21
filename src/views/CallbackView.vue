<script setup>
import { ref } from "vue";

// posts database
const postID = ref(0);
const posts = ref([]);

// fetched data
const data = ref([]);

function getPosts() {
  console.log("getPosts");

  setTimeout(() => {
    data.value = [];
    posts.value.forEach((post) => {
      data.value.push(post);
    }, 10);
  });
}

function createPost(post, callback, interval = 2000) {
  console.log("createPost");
  setTimeout(() => {
    posts.value.push({ id: postID.value, ...post });
    postID.value++;

    callback();
  }, interval);
}

createPost({ title: "Post One", body: "This is Post One" }, getPosts);
createPost({ title: "Post Two", body: "This is Post Two" }, getPosts);
createPost({ title: "Post Three", body: "This is Post Three" }, getPosts);
//getPosts();
</script>

<template>
  <div class="about">
    <h2>Posts</h2>
    <ul>
      <li v-for="post in posts" v-bind:key="post.id">
        {{ post }}
      </li>
    </ul>

    <h2>Data</h2>
    <ul>
      <li v-for="post in data" v-bind:key="post.id">
        {{ post }}
      </li>
    </ul>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
