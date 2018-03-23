<template>
  <div>
    <h1>{{ title }}</h1>
    <hr>
    <button @click="goHome" class="btn btn-primary">{{ anchor }}</button>
    <hr>
    <transition
      name="slide"
      mode="out-in">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        title: "The User page",
        anchor: "Go home",
        redirect: "/",
      }
    },
    methods: {
      goHome() {
        this.$router.push(this.redirect)
      }
    }
  }
</script>

<style scoped>
  .slide-enter {
    opacity: 0;
  }
  .slide-enter-active {
    animation: slide-in 1s ease-out forwards;
  }
  .slide-leave {

  }
  .slide-leave-active {
    animation: slide-out .7s ease-out;
  }

  @keyframes slide-in {
    from {
      transform: translateX(-20em);
      opacity: 0;
    }
    to {
      transform: translateX(0);
    }
  }

  @keyframes slide-out {
    from {
      transform: translateX(0);
    }
    to {
      transform: translateX(-20em);
      opacity: 0;
    }
  }
</style>
