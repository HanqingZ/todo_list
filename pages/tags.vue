<template>
  <div>
    <h1>Please Select One Tag</h1>
    <ul>
      <li v-for="tag in tags" :key="tag.name">{{ tag.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tags: [
        { name: 'Personal', color: 'black' },
        { name: 'Official', color: 'blue' }
      ]
    }
  }
}
</script>

<style>
h1 {
  color: rgb(134, 135, 209);
}
</style>
