<template>
  <div>
    <h5 class="header">{{ myCategory }} News</h5>

    <ul v-if="categoryLists && categoryLists.length">
      <li v-for="category in categoryLists" :key="category.title">
        <figure>
          <img :src="category.urlToImage" :alt="category.title" />
          <h4>{{category.title}}</h4>
          <figcaption>{{category.content}}</figcaption>
          <p>
            <a :href="category.url">Read more..</a>
          </p>
        </figure>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class ApiDetails extends Vue {
  categoryLists = [];

  created() {
    fetch(
      ` http://newsapi.org/v2/top-headlines?country=nl&category=${this.$route.params.category}&apiKey=d94efa04117b41ddaeb36bffcb564496`
    )
      .then(response => response.json())

      .then(data => (this.categoryLists = data.articles.slice(0, 12)));
  }
  get myCategory() {
    return (
      this.$route.params.category[0].toUpperCase() +
      this.$route.params.category.slice(1).toLowerCase()
    );
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-flow: row wrap;
}
li {
  flex: 0 0 90%;
  margin-left: 4%;
  margin-right: 0%;
  margin-bottom: 10px;

  border: 1px solid gray;
}
a {
  color: #42b983;
}

.header {
  margin-top: 70px;
}
li img {
  width: 100%;
  max-width: 300px;
  max-height: 200px;
}
/*  */
@media only screen and (min-width: 550px) {
  li {
    flex: 0 0 44%;
  }
}
@media only screen and (min-width: 850px) {
  li {
    flex: 0 0 20%;
  }
}
</style>
