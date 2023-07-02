<template>
  <div>
    items:
    <ul>
      <li v-for="item in items" :key="item.message">
        {{ item.message }}
      </li>
    </ul>
    object:
    <ul>
      <li v-for="(value, name, index) in object" :key="value">
        {{ index }}. {{ name }}: {{ value }}
      </li>
    </ul>
    evenNumbers:
    <ul>
      <li v-for="n in evenNumbers" :key="n">{{ n }}</li>
    </ul>
    sets:
    <ul v-for="set in sets" :key="set">
      <li v-for="n in even(set)" :key="n">{{ n }}</li>
    </ul>
    todos:
    <div id="todo-list-example">
      <form v-on:submit.prevent="addNewTodo">
        <label for="new-todo">Add a todo</label>
        <input v-model="newTodoText" id="new-todo" placeholder="E.g. Feed the cat" />
        <button>Add</button>
      </form>
      <ul>
        <li is="todo-item" v-for="(todo, index) in todos" v-bind:key="todo.id" v-bind:title="todo.title"
          v-on:remove="todos.splice(index, 1)">
        </li>
      </ul>
    </div>
  </div>
</template>
<script>

import Vue from 'vue';
const TodoItem = Vue.component('todo-item', {
  props: ['title'],
  template: `<li>
      {{ title }}
      <button v-on:click="$emit('remove')">Remove</button>
    </li>`
})

export default {
  name: 'VFor',
  components: {
    TodoItem
  },
  data: function () {
    return {
      items: [
        { message: 'Foo' },
        { message: 'Bar' },
      ],
      object: {
        title: 'How to do lists in Vue',
        author: 'Jane Doe',
        publishedAt: '2016-04-10',
      },
      numbers: [1, 2, 3, 4, 5],
      sets: [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]],
      newTodoText: '',
      todos: [
        { id: 1, title: 'Do the dishes', },
        { id: 2, title: 'Take out the trash', },
        { id: 3, title: 'Mow the lawn' },
      ],
      nextTodoId: 4,
    }
  },
  computed: {
    evenNumbers: function () {
      return this.numbers.filter(number => number % 2 === 0)
    }
  },
  methods: {
    even: function (numbers) {
      return numbers.filter(number => number % 2 === 0)
    },
    addNewTodo: function () {
      if (this.newTodoText) {
        this.todos.push({
          id: this.nextTodoId++,
          title: this.newTodoText,
        })
        this.newTodoText = ''
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>