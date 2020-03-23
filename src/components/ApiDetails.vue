<template>
  <div>
    <div v-if="lists && lists.length">
      <!-- <li v-for="item in lists" :key="item.API">{{item.Description}}</li> -->
      <h1>Description:{{myItem.Description}}</h1>
      <h3></h3>
      <ul v-if="relevantItems">
        <li v-for="(item,index) in relevantItems" :key="index">{{item.Description}}</li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class ApiDetails extends Vue {
  lists = [];

  created() {
    fetch("https://api.publicapis.org/entries?category=health")
      .then(response => response.json())
      .then(json => (this.lists = json.entries.slice(0, 10)));
  }

  get myItem() {
    return this.lists.find(item => item["API"] === this.$route.params.API);
  }
  get relevantItems() {
    return this.lists
      .filter(item => item["API"] != this.$route.params.API)
      .sort(() => Math.random() - Math.random())
      .slice(0, 3);
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
