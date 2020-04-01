<template>
  <div class="details">
    <div v-if="lists && lists.length">
      <div class="container">
        <b-card no-body class="overflow-hidden" style="max-width: 540px;">
          <b-row no-gutters>
            <b-col md="12">
              <b-card-img :src="myArticle.urlToImage" class="rounded-0"></b-card-img>
            </b-col>
            <b-col md="12">
              <b-card-body>
                <h4>
                  <b-card-text>{{ myArticle.title }}</b-card-text>
                </h4>

                <b-card-text>{{ myArticle.content }}</b-card-text>
                <a :href="myArticle.url">Read more..</a>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </div>
    </div>

    <h3>Relevant Articles</h3>
    <div class="newslist">
      <div class="container">
        <ul class="media-list">
          <li class="media" v-for="article in relevantArticles" :key="article.title">
            <div class="media-left">
              <a v-bind:href="article.url" target="_blank">
                <img class="media-object" v-bind:src="article.urlToImage" />
              </a>
            </div>
            <div class="media-body">
              <h4 class="media-heading">
                <a v-bind:href="article.url" target="_blank">
                  {{
                  article.title
                  }}
                </a>
              </h4>
              <h5>
                <i>by {{ article.author }}</i>
              </h5>
              <p>{{ article.description }}</p>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class ApiDetails extends Vue {
  lists = [];

  created() {
    fetch(
      "https://newsapi.org/v2/top-headlines?country=nl&apiKey=d94efa04117b41ddaeb36bffcb564496"
    )
      .then(response => response.json())
      .then(data => (this.lists = data.articles.slice(0, 10)));
  }

  get myArticle() {
    return this.lists.find(
      (item, index) => index === parseInt(this.$route.params.index)
    );
  }
  get relevantArticles() {
    return this.lists
      .filter((item, index) => index != parseInt(this.$route.params.index))
      .sort(() => Math.random() - Math.random())
      .slice(1, 4);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.media-object {
  width: 128px;
  padding: 10px;
}
.media {
  border-top: 1px solid lightgray;
  padding-top: 20px;
}
.details {
  margin-top: 30px;
}
</style>
