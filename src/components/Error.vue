<template>
  <div>
    <h1>{{ title }}</h1>
    <hr>
    <button
      @click="goHome"
      class="btn btn-primary"
      >{{ anchor }}</button>
  </div>
</template>

<script>
  import { eventBus } from '../utils/eventBus'

  export default {
    data() {
      return {
        title: "This is Error Page",
        anchor: "Go home",
        redirect: "/"
      }
    },
    methods: {
      goHome() {
        this.$router.push(this.redirect)
      }
    }
  }
</script>
