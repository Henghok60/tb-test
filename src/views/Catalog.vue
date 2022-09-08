<template>
  <div class="container my-5">
    <div class="d-flex py-3 justify-content-between align-items-center">
      <h5 class="title">COUNTRIES</h5>
      <div class="d-flex">
        <input
          v-model="searchBox"
          placeholder="Enter your name"
          class="w-50 m-2 form-control"
        />
        <button class="btn btn-primary m-2" @click="searchName(searchBox)">
          search
        </button>
        <b-dropdown id="dropdown-1" text="Dropdown Button" class="m-2">
          <b-dropdown-item>Desc</b-dropdown-item>
          <b-dropdown-item>Asc</b-dropdown-item>
        </b-dropdown>
      </div>
    </div>

    <div class="p-4">
      <paginate name="data" :list="items" :per="25" v-model="currentPage">
        <ul class="px-0">
          <Header></Header>
          <li
            v-for="(item, index) in paginated('data')"
            v-bind:key="index"
            :current-page="currentPage"
          >
            <Row :item="item" :index="index"></Row>
          </li>
        </ul>
      </paginate>
      <paginate-links for="data" :show-step-links="true" :v-model="currentPage">
      </paginate-links>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Row from "../components/Row.vue";
import Header from "../components/Header.vue";

export default {
  name: "Catalog",
  data() {
    return {
      rows: 0,
      perPage: 25,
      currentPage: 1,
      totalPages: 1,
      items: [],
      paginate: ["data"],
      searchBox: "",
    };
  },
  methods: {
    modalId: (id) => {
      return "modal-" + id;
    },
    async searchName(name) {
      try {
        const { data } = await axios.get(
          `https://restcountries.com/v3.1/name/${name}`
        );
        if (data) {
          this.items = data;
          this.currentPage = 1;
        }
      } catch (e) {
        return (this.items = []);
      }
    },
  },
  async mounted() {
    const { data } = await axios.get("https://restcountries.com/v3.1/all");
    this.items = data;
    this.rows = data.length;
  },
  components: { Row, Header },
};
</script>

<style>
.title {
  margin: 0;
}
ul {
  list-style-type: none;
}
.myActiveBtn {
  background-color: green;
}

ul.paginate-links > li.disabled > a {
  /* it doesn't work */
  color: red;
}
ul.paginate-links > li.number > a {
  /* it doesn't work, too */
  color: blue;
}

.paginate-links {
  display: flex;
  justify-content: center;
}

.paginate-links li {
  margin-right: 10px;
  cursor: pointer;
}

.w-5 {
  width: 50%;
}
</style>
