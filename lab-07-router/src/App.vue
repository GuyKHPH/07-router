<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h1>ShopVue</h1>
      </div>

      <v-spacer></v-spacer>

      <v-btn href="/" text>
        <span class="mx-1">Home</span>
      </v-btn>
      <v-btn href="/about" text>
        <span class="mx-1">About</span>
      </v-btn>
      <v-btn href="/shop" text>
        <span class="mx-1">Shop</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
