<template>
  <v-app>
    <v-app-bar app>
      <v-bar-title app>
        <h1 color="black">O'Blog <span class="text-md-body-1 font-italic">par Laurent</span></h1>
      </v-bar-title>

      <v-btn
        class="ma-2 pa-2"
        v-for="category of categories"
        :key="category._id"
      >
        {{ category._label }}
      </v-btn>

    </v-app-bar>

    <v-main >
      <v-container class="d-flex flex-wrap justify-space-around">


          <v-card
            v-for="post of posts"
            :key="post.id"
            elevation="10"
            class="ma-1"
            width="30%"
            outlined
            tile
          >

            <v-card-title
              ><h2>{{ post._title }}</h2></v-card-title
            >
            <v-card-subtitle>{{ post._slug }}</v-card-subtitle>
            <v-card-text>{{ post._content }}</v-card-text>

          </v-card>


      </v-container>
    </v-main>
    <v-footer app>
      <span class="text-center">Conception Breccan et fils... Irlande :-D</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      categories: [],
    };
  },

  methods: {
    async getAll() {
      const result = await fetch(
        "https://oblog-sinbad-laurent.herokuapp.com/v1/post"
      );
      const data = await result.json();
      this.posts = data;
      console.log(this.posts);
    },
  },

  async mounted() {
    try {
      const posts = await fetch(
        "https://oblog-sinbad-laurent.herokuapp.com/v1/post"
      );

      const categories = await fetch(
        "https://oblog-sinbad-laurent.herokuapp.com/v1/categorie"
      );

      const categoriesData = await categories.json();
      const postsData = await posts.json();
      this.posts = postsData;
      this.categories = categoriesData;
    } catch (err) {
      console.error(err);
    }
  },
};
</script>
