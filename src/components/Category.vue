<template>
  <div class="hello">
    <h1>categories</h1>
    <ul v-if="categories && categories.length">
      <li v-for="(category,index) of categories" :key="index">{{index}}: {{category}}</li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Category extends Vue {
  categories = [];

  created() {
    fetch("https://api.publicapis.org/categories")
      .then(response => response.json())
      .then(data => (this.categories = data));
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
</style>