<template>
  <div class="hello">
    <h1>Posts</h1>

    <button @click="sortByAZ('API')">Sort By A-Z</button>
    <button @click="sortByZA('API')">Sort by Z-A</button>
    <ul v-if="lists && lists.length">
      <li v-for="item of lists" :key="item.API">
        <router-link v-bind:to="'/details/' + item.API">{{ item.API }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  lists = [];
  firstName = "Semih";
  lastName = "Kasimoglu";
  counter = 0;

  created() {
    fetch("https://api.publicapis.org/entries?category=health")
      .then(response => response.json())
      .then(data => (this.lists = data.entries.slice(0, 10)));
  }

  //computed
  get fullName(): string {
    return this.firstName + " " + this.lastName;
  }

  //method
  incrementCounter() {
    this.counter = Math.floor(Math.random() * 10) + 1;
  }
  sortByAZ(prop: string) {
    this.lists.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
  }
  sortByZA(prop: string) {
    this.lists.sort((a, b) => (a[prop] < b[prop] ? 1 : -1));
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
