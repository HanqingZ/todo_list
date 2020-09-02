<template>
  <div class="main">
    <div class="sidebar">
      <ul class="tagList">
        <button
          v-for="(tag, index) in tags"
          :key="index"
          @click="showSelected(tag.name)"
        >
          {{ tag.name }}
        </button>
      </ul>
    </div>
    <div class="container">
      <logo />
      <h1 class="title">
        Todo List
      </h1>
      <div>
        <input v-model="newTodo" type="text" />
        <button class="add" @click="addNewTodo">+</button>
      </div>
      <ul class="todoList">
        <li
          v-for="(todo, index) in presentList"
          :key="index"
          :style="getColor(todo.tag)"
        >
          {{ todo.name }}
          <button>Done</button>
          <button>Delete</button>
        </li>
      </ul>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      tags: [
        { name: 'All', color: 'black' },
        { name: 'Personal', color: 'red' },
        { name: 'Official', color: 'blue' }
      ],
      newTodo: '',
      presentList: [],
      todoList: [{ name: 'hello world', tag: 'Personal' }]
    }
  },
  computed: {
    backgroundURL() {
      return require('../assets/images/background.jpeg')
    }
  },
  mounted() {
    this.presentList = this.todoList
  },
  methods: {
    getColor(tag) {
      return this.tags.map((e) => {
        if (e.name === tag) {
          return { color: e.color }
        }
      })
    },
    addNewTodo() {
      if (this.newTodo) {
        this.todoList.push({ name: this.newTodo, tag: '' })
        return (this.presentList = this.todoList)
      }
      return this.presentList
    },
    showSelected(selectedTag) {
      if (selectedTag === 'All') {
        return (this.presentList = this.todoList)
      }
      console.log(selectedTag)
      this.presentList = this.todoList.filter((e) => e.tag === selectedTag)
      return this.presentList
    }
  }
}
</script>

<style>
.main {
  margin: 0 auto;
  height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-image: url('../assets/images/background.jpeg');
  background-position: center;
  background-size: auto 100vh;
}
.sidebar {
  background-color: rgba(247, 247, 247, 0.9);
  width: 100vw;
  top: 0;
  position: absolute;
}

.tagList {
  display: flex;
  flex-direction: row;
  list-style-type: none;
  padding: 0;
}

.tagList > button {
  background-color: rgba(247, 247, 247, 0.9);
  border: none;
  height: 30px;
  width: 80px;
}
.tagList > button::after {
  border: none;
}

.container {
  background-color: rgba(247, 247, 247, 0.9);
  max-height: 100vh;
  max-width: 90vw;
  border-radius: 30px;
  align-content: center;
  padding: 20px;
  top: 20vh;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.add {
  border-radius: 50%;
}
.add::after {
  background-color: none;
}

.todoList {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  padding: 20px 0;
  color: #526488;
  list-style-type: none;
  min-height: 40px;
}

.subtitle {
  font-weight: 300;
  font-size: 25px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
