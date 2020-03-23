<template>
  <div class="hello">
    <h1>Random Item</h1>
    <ul v-if="randomItem && randomItem.length">
      <li v-for="item of randomItem" :key="item.API">
        <div>
          <h2>{{item.API}}</h2>
          <h3>{{item.Description}}</h3>
        </div>
      </li>
    </ul>

    <button @click="showAnother()">Another Item</button>
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
    fetch("https://api.publicapis.org/random")
      .then(response => response.json())
      .then(data => (this.randomItem = data.entries.slice(0)));
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
</style>