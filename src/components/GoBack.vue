<template>
  <span class="go-back">
    <b-button size="sm" variant="secondary" @click="goback">enrere</b-button>
  </span>
</template>

<script>
export default {
  methods: {
    goback() {
      return this.$router.go(-1);
    },
  },
};
</script>

<style></style>
