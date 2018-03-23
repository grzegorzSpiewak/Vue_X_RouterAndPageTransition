<template>
  <div>
  <p>Please select a User</p>
  <hr>
    <ul class="list-group">
      <transition-group
        name="slide-list"
        appear>
        <router-link
          v-for="user in users"
          :to="{ path: `/user/${user.id}`}"
          :key="`${user.id}`"
          tag="li"
          class="list-group-item">
          {{ user.user }}
        </router-link>
      </transition-group>
    </ul>
    <button
      class="btn btn-primary"
      @click="addUser">
      Add user
    </button>
    <button
      v-if="users.length > 0"
      class="btn btn-primary"
      @click="removeUser">
      Remove user
    </button>
  </div>
</template>

<script>
  import { eventBus} from '../../utils/eventBus.js'
  export default {
    data() {
      return {
        users: [
          { user: "User", id: "1"},
          { user: "User", id: "2"},
          { user: "User", id: "3"},
          { user: "User", id: "4"},
        ]
      }
    },
    methods: {
      addUser() {
        let newUserId = this.users.length + 1
        let data = this.handleData('New user', newUserId)
        this.users.push(data)
        eventBus.$emit('userWasAdded', data)
      },
      removeUser() {
        let data = {}

        if (this.users.length > 0) {
          let removedUser = this.users.pop(-1)
          data = this.handleData(removedUser.user, removedUser.id)
          eventBus.$emit('userWasRemoved', data)
        } else {
          alert("No more users")
        }
      },
      handleData(user, id) {
        let data = {
          user: user,
          id: id,
          show: true
        }
        return data
      }
    },
  }
</script>

<style scoped>
  ul {
    height: 20em;
    overflow: auto;
  }
  ul::-webkit-scrollbar {
    display: none;
  }
  ul li:hover {
    background-color: #d3d3d3;
    cursor: pointer;
  }
  .slide-list-enter {
    opacity: 0;
  }
  .slide-list-enter-active {
    animation: slide-list-in 1s ease-out forwards;
  }
  .slide-list-leave {

  }
  .slide-list-leave-active {
    animation: slide-list-out .7s ease-out;
  }

  @keyframes slide-list-in {
    from {
      transform: translateX(20em);
      opacity: 0;
    }
    to {
      transform: translateX(0);
    }
  }

  @keyframes slide-list-out {
    from {
      transform: translateX(0);
    }
    to {
      transform: translateX(20em);
      opacity: 0;
    }
  }
</style>
