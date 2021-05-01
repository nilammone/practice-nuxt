<template>
  <div>
    <v-container>
      <h2>Photos pages</h2>
      <v-row style="height: 150px">
        <v-col v-for="photo in photos" :key="photo.id">
          <v-card class="pa-2" outlined tile>
            <v-card class="mx-auto" max-width="344">
              <nuxt-link :to="`/photos/${photo.id}`">
                <p>{{ photo.id }}</p>
                <p>By: {{ photo.author }}</p>
              </nuxt-link>
            </v-card>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const BASE_URL = 'https://picsum.photos'

    const photos = await $axios.$get(`${BASE_URL}/v2/list`)

    return { photos }
  },
}
</script>

<style></style>
