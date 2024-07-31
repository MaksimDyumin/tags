<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>
    </v-app-bar>

    <v-main>
      <div class="tags__fullsize-container">
        <v-divider></v-divider>
        <TagList :tags="tags" :alignment="'start'"/>
        <v-divider></v-divider>
        <TagList :tags="tags" :alignment="'space-between'"/>
        <v-divider></v-divider>
        <TagList :tags="tags" :alignment="'end'"/>
        <v-divider></v-divider>
      </div>

      <div class="tags__halfsize-container">
        <v-divider></v-divider>
        <TagList :tags="tags" :alignment="'start'"/>
        <v-divider></v-divider>
        <TagList :tags="tags" :alignment="'space-between'"/>
        <v-divider></v-divider>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import TagList from './components/TagList.vue';


export default {
  name: 'App',

  components: {
    TagList
  },

  data: () => ({
    tags: [
      {
        id: 1,
        text: 'dasdasdsad',
        icon: 'mdi-minus-circle'
      },
      {
        id: 2,
        text: 'qrwreqwrqrqwesad da sada sada da eawe asrfa'
      },
      {
        id: 3,
        text: '14325'
      },
    ]
  }),
};
</script>

<style>
.tags__container{
  margin-top: 12px;
  padding: 20px;
}
.tags__halfsize-container {
  width: 50%;
  margin-top: 40px;
}
</style>