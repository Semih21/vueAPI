<template>
  <div>
    <h1>Details</h1>
    <ApiDetails />
  </div>
</template>

<script>
// @ is an alias to /src
import ApiDetails from "@/components/ApiDetails.vue";

export default {
  name: "Details",
  components: {
    ApiDetails
  }
};
</script>
