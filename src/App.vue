<script>
import TodoItem from './components/TodoItem.vue';
import { nanoid } from 'nanoid';

export default {
  name: "app",
  components: {
    TodoItem,
  },
  data(){
return {
  TodoItems:[
    {id:"todo-"+nanoid(), label: "Task 1" , done: false},
    {id:"todo-"+nanoid(), label: "Task 2" , done: false},
    {id:"todo-"+nanoid(), label: "Task 3" , done: false},
    {id:"todo-"+nanoid(), label: "Task 4" , done: false},
],
};
  },
};

</script>

<template>
  <div id="app">
    <h1>
      To-Do List
    </h1>
      <ul>
        <li v-for="item in TodoItems"  v-bind:key="item.id">
          <todo-item v-bind:label="item.label" v-bind:done="item.done"></todo-item>
        </li>
      </ul>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
