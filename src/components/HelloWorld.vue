<template>
  <div class="hello">
    <h2>News Articles</h2>SORT BY:
    <b-button class="btn" variant="primary" @click="sortByTitle('title')">Title</b-button>
    <span>&emsp;</span>
    <b-button class="btn" variant="danger" @click="sortByAuthor('author')">Author</b-button>

    <ul v-if="lists && lists.length">
      <li v-for="(item, index) of lists" :key="index">
        <div class="story">
          <router-link v-bind:to="'/details/' + index">{{ index + 1 }}-{{ item.title }}</router-link>
          <br />
          <span class="meta">by {{ item.author }} | publisled at {{ item.publishedAt }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  lists = [];

  created() {
    fetch(
      "https://newsapi.org/v2/top-headlines?country=nl&apiKey=d94efa04117b41ddaeb36bffcb564496"
    )
      .then(response => response.json())
      .then(data => (this.lists = data.articles.slice(0, 10)));
  }

  sortByTitle(prop: string) {
    this.lists.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
  }
  sortByAuthor(prop: string) {
    this.lists.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  margin-top: 70px;
}
.story {
  background-color: #fff;
  padding: 10px 30px 10px 50px;
  border-bottom: 1px solid #eee;
  position: relative;
  line-height: 20px;
}

.story a {
  color: #34495e;
  font-weight: 600;
  text-decoration: none;
}

.story .meta {
  font-size: 0.85em;
  color: #828282;
}
</style>
