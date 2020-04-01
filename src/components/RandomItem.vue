<template>
  <div v-if="randomItem">
    <div v-for="item in randomItem" :key="item.title" class="random-container">
      <b-card no-body class="overflow-hidden" style="max-width: 540px;">
        <b-row no-gutters>
          <b-col md="12">
            <b-card-img :src="item.urlToImage" :width="260" :height="260" class="rounded-0"></b-card-img>
          </b-col>
          <b-col md="12">
            <b-card-body>
              <h4>
                <b-card-text>{{ item.title }}</b-card-text>
              </h4>

              <b-card-text>{{ item.content }}</b-card-text>
              <p>
                <a :href="item.url">Read more..</a>
              </p>

              <b-button class="btn" variant="primary" @click="showAnother()">Another News</b-button>
            </b-card-body>
          </b-col>
        </b-row>
      </b-card>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class RandomItem extends Vue {
  randomItem = [];

  created() {
    this.fetchData();
  }

  fetchData() {
    fetch(
      "https://newsapi.org/v2/top-headlines?country=nl&apiKey=d94efa04117b41ddaeb36bffcb564496"
    )
      .then(response => response.json())
      .then(
        data =>
          (this.randomItem = data.articles
            .sort(() => Math.random() - Math.random())
            .slice(0, 1))
      );
  }
  showAnother() {
    return this.fetchData();
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
.random-container {
  margin-top: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
