<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animated routing with Vue</h1>
                <hr>
                <appHeader />
                <transition name="fade" mode="out-in">
                  <router-view></router-view>
                </transition>
                <notification />
            </div>
        </div>
    </div>
</template>

<script>
    import Header from './components/Header.vue'
    import NotificationWindow from './components/Notification.vue'

    export default {
      components: {
        appHeader: Header,
        notification: NotificationWindow
      }
    }
</script>

<style scoped>
  .container {
    height: 100vh;
    width: 100%;
    overflow: hidden;
  }
  .fade-enter {
    opacity: 0;
  }
  .fade-enter-active {
    transition: all .5s;
  }
  .fade-leave {

  }
  .fade-leave-active {
    transition: all .5s;
    opacity: 0;
  }
</style>
