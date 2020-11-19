<template>
  <div>
        <div class="d-flex justify-content-between px-5 bg-info py-4 border rounded">
            <div class="input-group">
                <input v-model="title" type="text" class="form-control" placeholder="Add new todo" aria-label="Recipient's username" aria-describedby="button-addon2">
                <div class="input-group-append">
                    <button @click="addTodo" class="btn btn-primary" type="button" id="button-addon2">Add</button>
                </div>
            </div>
        </div>
        <ul class="d-block w-100 px-5">
          <li v-for="(todo, index) in todos" :key="index" class="d-flex justify-content-between my-3 border-bottom pb-1">
            <div>{{ todo.title}}</div>
            <div>
                <input v-if="todo.completed" type="checkbox" checked @click="toggleCompleted(todo)">
                <input v-if="!todo.completed" type="checkbox" @click="toggleCompleted(todo)">
            </div>
          </li>
        </ul>
        <div class="clearfix"></div>
        <div class="row px-5 mt-4">
            <strong>Total todos: &nbsp; </strong> {{ todos.length - completedTodos + '/' + todos.length }}
        </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            todos: [],
            title: ''
        }
    },

    async fetch() {
        this.todos = [
            {
                    title: 'Drop kids to school',
                    completed: true
                },
                {
                    title: 'Grocery',
                    completed: false
                },
                {
                    title: 'Visit doctor',
                    completed: false
                },
                {
                    title: 'Call to mom',
                    completed: false
                }
        ]
    },

    computed: {
        completedTodos() {
            return this.todos.filter(todo => todo.completed).length
        }
    },

    methods: {
        toggleCompleted(todo) {
            let todoIndex = this.todos.indexOf(todo)
            this.todos[todoIndex].completed = this.todos[todoIndex].completed ? false : true
        },

        addTodo() {
            if(!this.title) return

            this.todos.push({title: this.title, completed: false})
            this.title = ''
        }
    }
}
</script>

<style>
</style>