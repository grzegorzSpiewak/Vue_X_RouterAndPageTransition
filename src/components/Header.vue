<template>
  <ul class="nav nav-pills">
    <router-link
      v-for="item in menu"
      tag="li"
      :to="item.path"
      active-class="active"
      exact>
      <a>{{ item.anchor }}</a>
      </router-link>
  </ul>
</template>


<script>
  export default {
    data() {
      return {
        menu: [
          { anchor: 'Home', path: "/" },
          { anchor: 'User', path: "/user" },
        ]
      }
    }
  }
</script>
