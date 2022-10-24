<template>
  <header>
    <h1>Header</h1>
    <div>
      {{ propsdata }}

      <button v-on:click="clickEvent">click</button>
    </div>
  </header>
</template>

<script>
export default {
  props: ["propsdata"],
  methods: {
    clickEvent: function () {
      this.$emit("renew");
    },
  },
};
</script>

<style>
</style>