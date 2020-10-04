<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination pagination-sm">
      <!-- move to first page -->
      <li
        class="page-item"
        :class="page === 1 ? 'disabled cursor-not-allowed' : 'cursor-pointer'"
        @click="pageClick(1)"
      >
        <a class="page-link" tabindex="-1">First</a>
      </li>

      <li
        class="page-item"
        v-for="index in totalPages()"
        :key="index"
        @click="pageClick(index)"
        :class="
          page === index ? 'disabled cursor-not-allowed' : 'cursor-pointer'
        "
      >
        <a class="page-link">{{ index }}</a>
      </li>

      <!-- move to last page -->
      <li
        class="page-item"
        :class="
          page === totalPages()
            ? 'disabled cursor-not-allowed'
            : 'cursor-pointer'
        "
        @click="pageClick(totalPages())"
      >
        <a class="page-link">Last</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    page: Number,
    limit: Number,
    count: Number,
  },
  methods: {
    totalPages() {
      return Math.ceil(this.count / this.limit);
    },
    pageClick(page) {
      if (page !== this.page) this.$emit("pageChanged", page);
    },
  },
};
</script>

<style scoped>
.cursor-pointer {
  cursor: pointer;
}
.cursor-not-allowed {
  cursor: not-allowed;
}
</style>