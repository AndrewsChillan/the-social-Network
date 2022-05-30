<template>
  <div>
    <p>Page actuelle = {{ page + 1 }}/{{ totalPages }}</p>
    <button
      v-for="number in totalPages"
      :key="number"
      @click="changePage(number - 1)"
    >
      {{ number }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      page: 0,
    };
  },
  props: {
    totalPages: Number,
  },
  emits: ["page-change"],
  methods: {
    changePage(number) {
      this.$emit("page-change", number);
    },
  },
};
</script>
