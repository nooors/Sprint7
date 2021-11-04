<template>
  <span class="go-back">
    <button size="sm" variant="secondary" @click="goback"><<< enrere</button>
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

<style lang="sass">
.go-back
  button 
    border: 0
    background-color: transparent
    font-size: .9rem !important
    &:hover
      color: #6c757d

</style>
