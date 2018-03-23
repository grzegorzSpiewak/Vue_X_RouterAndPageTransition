<template>
  <div>
    <h1>{{ title }}</h1>
    <hr>
    <p html>{{ content }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        title: "The home page",
        content: "Lorem ipsum dolor sit amet, consectetur adipisicing elit blanditiis consequunturdolore excepturi laborum maiores minima nihil non nulla obcaecati quas quibusdam quod sed suscipit verovoluptatem."
      }
    }
  }
</script>
