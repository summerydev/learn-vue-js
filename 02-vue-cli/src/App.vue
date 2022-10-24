<template>
  <div>
    <AppHeader v-bind:propsdata="headerDes" v-on:renew="renewStr"></AppHeader>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
export default {
  data: function () {
    return {
      headerDes: "hi",
    };
  },
  components: { AppHeader },
  methods: {
    renewStr: function () {
      this.headerDes = "headerDes changed";
    },
  },
};
</script>

<style>
</style>