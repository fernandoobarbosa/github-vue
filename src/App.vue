<template>
  <div id="app">
    <div class="container">
      <HelloWorld @filter="searchData" :users="users" />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import axios from "axios";
export default {
  data: () => ({
    users: [],
  }),
  name: "App",
  components: {
    HelloWorld,
  },
  methods: {
    async searchData(searchInput, page) {
      try {
        const { data } = await axios({
          method: "get",
          url:
            " https://api.github.com/search/repositories?q=" +
            searchInput.toLowerCase() +
            "&order=desc&page=" +
            page +
            "&per_page=10",
        });
        console.log(data);
        this.users = data.items;
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
