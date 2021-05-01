<template>
  <div>
    <v-container>
      <h2 class="title">Blog</h2>
      <v-row style="height: 150px">
        <v-col v-for="post in posts" :key="post.slug">
          <v-card class="pa-2" outlined tile>
            <v-card class="mx-auto" max-width="344">
              <nuxt-link :to="`/blog/${post.slug}`">
                {{ post.title }}
              </nuxt-link>

              <p>{{ post.description }}</p>

              <p>Create At: {{ post.createdAt }}</p>
            </v-card>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const posts = await $content('blog').sortBy('createdAt', 'desc').fetch()

    return { posts }
  },
}
</script>

<style></style>
