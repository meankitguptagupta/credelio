<template>
  <div class="container mt-2">
    <table class="table table-bordered">
      <thead>
        <tr class="text-center">
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Duration</th>
          <th scope="col">descriptions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in list" :key="index">
          <td>{{ getIndex(index) }}</td>
          <td>
            <div class="media">
              <img
                :src="item.poster"
                class="mr-3 img-thumbnail poster"
                :alt="item.name"
              />
              <div class="media-body">
                <h5 class="mt-0 text-capitalize">{{ item.name }}</h5>
              </div>
            </div>
          </td>
          <td>{{ item.duration }}</td>
          <td class="text-capitalize">{{ item.desc }}</td>
        </tr>
      </tbody>
    </table>

    <div class="pull-right">
      <Pagination :page="page" :limit="limit" :count="count" @pageChanged="pageChanged"/>
    </div>
  </div>
</template>

<script>
const faker = require("faker");

import Pagination from "./pagination";

export default {
  components: {
    Pagination,
  },
  data() {
    return {
      list: [],
      page: 1,
      limit: 10,
      count: Math.ceil(Math.random() * 100),
    };
  },
  created() {
    this.listMovies();
  },
  methods: {
    listMovies() {
      this.list = []
      for (let i = 1; i <= this.limit; i++) {
        this.list.push({
          name: faker.name.findName(),
          year: faker.date.past(),
          poster: this.getRandomImg(),
          desc: faker.lorem.sentence(),
          duration: this.getRandom(150, 30),
        });
      }
    },
    getIndex(index) {
      return (this.page - 1) * this.limit + (index + 1);
    },
    getRandom(max, min) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    getRandomImg() {
      let fns = [
        faker.image.imageUrl,
        faker.image.image,
        faker.image.image,
        faker.image.avatar,
        faker.image.imageUrl,
        faker.image.abstract,
        faker.image.animals,
        faker.image.business,
        faker.image.cats,
        faker.image.city,
        faker.image.food,
        faker.image.nightlife,
        faker.image.fashion,
        faker.image.people,
        faker.image.nature,
        faker.image.sports,
        faker.image.technics,
        faker.image.transport,
        faker.image.dataUri,
        faker.image.lorempixel,
        faker.image.unsplash,
      ];

      let num = Math.floor(Math.random() * fns.length)
      if (!num)
        num = 0

      // calling function randomly
      return fns[num]();
    },
    pageChanged(page) {
      this.page = page
      this.listMovies()
    }
  },
};
</script>

<style scoped>
.poster {
  width: 100px;
}
</style>