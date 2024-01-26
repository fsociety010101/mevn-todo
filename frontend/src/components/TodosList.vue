<template>
    <div class="list row">
        <div class="col-md-8">
            <div class="input-group mb-3">
                <input type="text" class="form-control" placeholder="Search by title" v-model="title" />
                <div class="input-group-append">
                    <button class="btn btn-outline-secondary ms-1" type="button" @click="searchTitle">
                        Search
                    </button>
                </div>
            </div>
        </div>
        <div class="col-md-6">
            <h4>Todos List</h4>
            <ul class="list-group">
                <li class="list-group-item" :class="{ active: index == currentIndex }" v-for="(todo, index) in todos"
                    :key="index" @click="setActiveTodo(todo, index)">
                    {{ todo.title }}
                </li>
            </ul>

            <button class="my-3 btn btn-sm btn-danger" @click="removeAllTodos">
                Remove All
            </button>
        </div>
        <div class="col-md-6">
            <div v-if="currentTodo">
                <h4>Todo</h4>
                <div>
                    <label><strong>Title:</strong></label> {{ currentTodo.title }}
                </div>
                <div>
                    <label><strong>Description:</strong></label> {{ currentTodo.description }}
                </div>
                <div>
                    <label><strong>Status:</strong></label> {{ currentTodo.published ? "Done" : "Pending" }}
                </div>
                <div>
                    <label><strong>Id:</strong></label> {{ currentTodo.id }}
                </div>

                <a class="btn btn-warning my-2" :href="'/todos/' + currentTodo.id">
                    Edit
                </a>
            </div>
            <div v-else>
                <br />
                <p>Please click on a Todo...</p>
            </div>
        </div>
    </div>
</template>

<script>
import TodoDataService from "../services/TodoDataService";

export default {
    name: "todos-list",
    data() {
        return {
            todos: [],
            currentTodo: null,
            currentIndex: -1,
            title: ""
        };
    },
    methods: {
        retrieveTodos() {
            TodoDataService.getAll()
                .then(response => {
                    this.todos = response.data;
                    console.log(response.data);
                })
                .catch(e => {
                    console.log(e);
                });
        },

        refreshList() {
            this.retrievetodos();
            this.currentTodo = null;
            this.currentIndex = -1;
        },

        setActiveTodo(todo, index) {
            this.currentTodo = todo;
            this.currentIndex = index;
        },

        removeAllTodos() {
            TodoDataService.deleteAll()
                .then(response => {
                    console.log(response.data);
                    this.refreshList();
                })
                .catch(e => {
                    console.log(e);
                });
        },

        searchTitle() {
            TodoDataService.findByTitle(this.title)
                .then(response => {
                    this.todos = response.data;
                    console.log(response.data);
                })
                .catch(e => {
                    console.log(e);
                });
        }
    },
    mounted() {
        this.retrieveTodos();
    }
};
</script>

<style>
.list {
    text-align: left;
    max-width: 750px;
    margin: auto;
}
</style>
