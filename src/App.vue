<script>
import TodoItem from './components/TodoItem.vue';
import { nanoid } from 'nanoid';
import TodoForm from './components/TodoForm.vue';


export default {
  name: "app",
  components: {
    TodoItem, TodoForm,
  },
  data(){
return {
  TodoItems:[
    {id:"todo-"+nanoid(), label: "Task 1" , done: false},
    {id:"todo-"+nanoid(), label: "Task 2" , done: false},
    {id:"todo-"+nanoid(), label: "Task 3" , done: true},
    {id:"todo-"+nanoid(), label: "Task 4" , done: false},
],
};
  },

  methods:{
     addTodo(todoLabel){
      this.TodoItems.push({id: "todo-" + nanoid(), label: todoLabel, done: false});
     },

     updateDoneStatus(toDoId) {
  const toDoToUpdate = this.TodoItems.find((item) => item.id === toDoId)
  toDoToUpdate.done = !toDoToUpdate.done
},

deleteToDo(toDoId) {
  const itemIndex = this.TodoItems.findIndex((item) => item.id === toDoId);
  this.TodoItems.splice(itemIndex, 1);
},

editToDo(toDoId, newLabel) {
  const toDoToEdit = this.TodoItems.find((item) => item.id === toDoId);
  toDoToEdit.label = newLabel;
}


  },

  computed: {
  listSummary() {
    const numberFinishedItems = this.TodoItems.filter((item) =>item.done).length;
    return `${numberFinishedItems} out of ${this.TodoItems.length} items completed`;
  }
}

};

</script>

<template>
  <div id="app">
    <h1>
      To-Do List
    </h1>
    <todo-form @todo-added="addTodo"></todo-form>
    <h2 id="list-summary">
      {{listSummary}}
    </h2>
      <ul aria-labelledby="list-summary" class="stack-large">
        <li v-for="item in TodoItems"  v-bind:key="item.id">
          <todo-item
            :label="item.label"
            :done="item.done"
            :id="item.id"
            @checkbox-changed="updateDoneStatus(item.id)"
            @item-deleted="deleteToDo(item.id)"
            @item-edited="editToDo(item.id, $event)">
          </todo-item>

        </li>
      </ul>
  </div>
</template>

<style>
  /* Global styles */
  .btn {
    padding: 0.8rem 1rem 0.7rem;
    border: 0.2rem solid #4d4d4d;
    cursor: pointer;
    text-transform: capitalize;
  }
  .btn__danger {
    color: #fff;
    background-color: #ca3c3c;
    border-color: #bd2130;
  }
  .btn__filter {
    border-color: lightgrey;
  }
  .btn__danger:focus {
    outline-color: #c82333;
  }
  .btn__primary {
    color: #fff;
    background-color: #000;
  }
  .btn-group {
    display: flex;
    justify-content: space-between;
  }
  .btn-group > * {
    flex: 1 1 auto;
  }
  .btn-group > * + * {
    margin-left: 0.8rem;
  }
  .label-wrapper {
    margin: 0;
    flex: 0 0 100%;
    text-align: center;
  }
  [class*="__lg"] {
    display: inline-block;
    width: 100%;
    font-size: 1.9rem;
  }
  [class*="__lg"]:not(:last-child) {
    margin-bottom: 1rem;
  }
  @media screen and (min-width: 620px) {
    [class*="__lg"] {
      font-size: 2.4rem;
    }
  }
  .visually-hidden {
    position: absolute;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px 1px 1px 1px);
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
  }
  [class*="stack"] > * {
    margin-top: 0;
    margin-bottom: 0;
  }
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* End global styles */
  #app {
    background: #fff;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow:
      0 2px 4px 0 rgb(0 0 0 / 20%),
      0 2.5rem 5rem 0 rgb(0 0 0 / 10%);
  }
  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>



