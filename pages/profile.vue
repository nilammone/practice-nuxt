<template>
  <div>
    <v-container>
      <h2 class="title text-center">My Profile</h2>
      <div class="d-flex justify-center mb-6">
        <img class="avatar" :src="user.avatar_url" alt="User Avatar" />
      </div>

      <p>Bio: {{ user.bio }}</p>
      <p>Location: {{ user.location }}</p>

      <v-row style="height: 150px">
        <v-col v-for="repo in repos" :key="repo.id">
          <v-card class="pa-2" outlined tile>
            <v-card class="mx-auto" max-width="344">
              <!-- <nuxt-link :to="repo.html_url">{{ repo.name }}</nuxt-link> -->
              <a :href="repo.html_url" target="_blank">{{ repo.name }}</a>
              <p>Star: {{ repo.stargazers_count }}</p>
            </v-card>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const baseURL = 'https://api.github.com'

    // set not sent token to github
    $axios.setHeader('Authorization', null)

    // set mutiple await
    const [user, repos] = await Promise.all([
      $axios.$get(`${baseURL}/users/phonbopit`),
      $axios.$get(`${baseURL}/users/phonbopit/repos`),
    ])

    // set single await
    // const user = await $axios.$get(`${baseURL}/users/phonbopit`)
    // const repos = await $axios.$get(`${baseURL}/users/phonbopit/repos`)

    return { user, repos }
  },
}
</script>

<style scoped>
.avatar {
  width: 128px;
  height: 128px;
}
</style>
