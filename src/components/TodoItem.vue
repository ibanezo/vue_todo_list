<template>
    <!-- we are binding class in condition completed -->
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <!-- we are adding event for the checkbox -->
            <input type="checkbox" v-on:change="markComplete">
            {{todo.title}}
            <!-- for deleting we should go to data in App.vue through Todos.vue (we go upwards),
                 we can do that with events @event -->
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>

<script>
    export default {
        name: "TodoItem",
        props: ["todo"],
        methods: {
            markComplete() {
                this.todo.completed = !this.todo.completed;
            }
        }
    }
</script>

<style scoped>
   .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #c55555;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }

</style>