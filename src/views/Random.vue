<template>
  <div class="home">
    <RandomItem />
  </div>
</template>

<script>
// @ is an alias to /src
import RandomItem from "@/components/RandomItem.vue";

export default {
  name: "Random",
  components: {
    RandomItem
  }
};
</script>