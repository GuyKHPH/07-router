<template>
  <v-container class="text-center">
    <h2 class="text-center">Detail</h2>
    <img :src="productimg" width="200px" height="200px" />
    <h2>Name product</h2>
    <h3>{{ producttitle }}</h3>
    <p class="text-start">{{ productdes }}</p>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      producttitle: this.$route.params.title,
      productdes: this.$route.params.description,
      productimg: this.$route.params.image,
    };
  },
};
</script>

<style></style>
