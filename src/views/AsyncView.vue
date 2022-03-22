<script setup>
import { ref } from "vue";

// posts database
const postIdRef = ref(0); // next id
const postsRef = ref([]);

// fetched data
const dataRef = ref([]);

const urlRef = ref("");
const responseRef = ref("");
const errorRef = ref("");

function onFetch() {
  console.log("onFetch");
  // const test = "https://jsonplaceholder.typicode.com/users/1";

  fetch(urlRef.value)
    .then((response) => response.json())
    .then((data) => (responseRef.value = data))
    .catch((error) => {
      console.error(error);
      errorRef.value = error;
    });

  // Promise.all([promise1]).then((values) => (response.value = values));
}

function getPosts() {
  console.log("getPosts");

  setTimeout(() => {
    dataRef.value = [];
    postsRef.value.forEach((post) => {
      dataRef.value.push(post);
    }, 10);
  });
}

function createPost(post, interval = 2000) {
  console.log("createPost");
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      postsRef.value.push({ id: postIdRef.value, ...post });
      postIdRef.value++;

      const error = false;

      if (!error) {
        resolve();
      } else {
        reject("Error message");
      }
    }, interval);
  });

  return promise;
}

/*
createPost({ title: "Post One", body: "This is Post One" })
  .then(getPosts)
  .catch((err) => console.error(err));
createPost({ title: "Post Two", body: "This is Post Two" })
  .then(getPosts)
  .catch((err) => console.error(err));
createPost({ title: "Post Three", body: "This is Post Three" })
  .then(getPosts)
  .catch((err) => console.error(err));
*/

async function init() {
  await createPost({ title: "Post One", body: "This is Post One" });

  getPosts();
}

async function fetchUsers() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await res.json();

  dataRef.value = data;
}

// init();
fetchUsers();
</script>

<template>
  <div class="about">
    <h2>Posts</h2>
    <ul>
      <li v-for="post in postsRef" v-bind:key="post.id">
        {{ post }}
      </li>
    </ul>

    <h2>Data</h2>
    <ul>
      <li v-for="post in dataRef" v-bind:key="post.id">
        {{ post }}
      </li>
    </ul>
  </div>

  <h2>Fetch</h2>
  <label>URL: </label>
  <input v-model="urlRef" />
  <button @click="onFetch">Fetch</button>
  <p>Request: {{ urlRef }}</p>
  <p>Response: {{ responseRef }}</p>
  <p>Error: {{ errorRef }}</p>
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
