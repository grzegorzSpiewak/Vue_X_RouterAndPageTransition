<template>
  <section class="notification">
    <transition-group name="pop" mode="in-out">
      <div
        v-for="notification in notifications"
        v-if="notification"
        :key="notification.id + notification.action"
        :class="notification.style">
          <h3>User name: {{ notification.user }}</h3>
          <h3>User id: {{ notification.id }}</h3>
          <h3>Action: {{ notification.action }}</h3>
      </div>
    </transition-group>
  </section>
</template>

<script>
  import { eventBus } from '../utils/eventBus'

  export default {
    data() {
      return {
        notifications: [],
      }
    },
    methods: {
      handleNotification(data) {
        this.notifications.unshift(data)
        setTimeout(() => { this.notifications.pop(data)}, 3000)
      },
      userWasAdded(data) {
        const action = "User was added"
        const style = "alert alert-success"

        let info = this.handleData(data, action, style)
        this.handleNotification(info, action)
      },
      userWasRemoved(data) {
        const action = "User was removed"
        const style = "alert alert-danger"

        let info = this.handleData(data, action, style)
        this.handleNotification(info, action)
      },
      handleData(data, action, style) {
        let info = {
          user: data.user,
          id: data.id,
          action: action,
          style: style
        }
        return info
      }
    },
    created() {
      eventBus.$on('userWasAdded', data => this.userWasAdded(data))
      eventBus.$on('userWasRemoved', data => this.userWasRemoved(data))
    }
  }

</script>

<style scoped>
  .notification {
    width: 250px;
    position: absolute;
    top: 10%;
    left: -35%;
    z-index: 1;
  }
  h3 {
    font-size: 1em;
    font-weight: 400;
    line-height: 1.5em;
    padding: 0;
    margin: 0;
  }
  .pop-enter {

  }
  .pop-enter-active {
    animation: popup .5s;
  }

  .pop-leave {

  }
  .pop-leave-active {
    animation: popout .5s;
  }

  @keyframes popup {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.4);
    }
    60% {
      transform: scale(1.1);
    }
    70% {
      transform: scale(1.2);
    }
    80% {
      transform: scale(1);
    }
    90% {
      transform: scale(1.1);
    }
    100% {
      transform: scale(1);
    }
  }

  @keyframes popout {
    0% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.2);
    }
    100% {
      transform: scale(0);
    }
  }
</style>
