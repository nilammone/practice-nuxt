<template>
  <div>
    <v-container>
      <h2 class="title">Photo Details</h2>
      <img class="image" :src="photo.download_url" alt="Photo Image" />
      <p>Author : {{ photo.author }}</p>
      <v-btn to="/photos">Back</v-btn>
    </v-container>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios, params }) {
    const photo = await $axios.$get(
      `https://picsum.photos/id/${params.id}/info`
    )
    return { photo }
  },
}
</script>

<style>
.image {
  width: 200px;
}
</style>
