<template>
  <div>
    <br />
    <!-- <input
      type="text"
      class="form-control"
      v-on:input="debounceInput"
      v-model="searchInput"
      placeholder="Please type here..."
    /> -->
    <i class="nes-octocat animate"></i>
    <div class="nes-field">
      <input
        type="text"
        id="name_field"
        class="nes-input"
        v-on:input="debounceInput"
        v-model="searchInput"
        placeholder="Please search a repository here..."
      />
    </div>

    <div v-for="n in users" :key="n.id">
      <!-- {{ n.login }} -->
      <br />
      <div class="nes-container is-rounded is-dark">
        <p>
          <a :href="n.html_url">{{ n.html_url }}</a>
        </p>
      </div>
    </div>

    <!-- <input type="text" v-on:input="debounceInput" v-model="searchInput" /> -->
    <div v-if="false">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item"><a class="page-link" href="#">Previous</a></li>

          <li class="page-item">
            <a class="page-link" href="#">Next</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    users: [],
  },
  data: function() {
    return {
      searchInput: "",
      filterKey: "",
      page: 0,
    };
  },
  methods: {
    // nextPage() {
    //   this.page = this.page + 1;
    //   this.$emit("filter", this.searchInput, this.page);
    // },
    debounceInput: _.debounce(function() {
      this.filterKey = this.searchInput;
      this.$emit("filter", this.searchInput, this.page);
      console.log(this.filterKey);
    }, 3000),
  },
};
</script>
