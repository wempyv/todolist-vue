<template>
  <div class="container">
    <div class="container">
      <div class="header mt-4">
        <h3 class="title">Welcome Back</h3>
        <p class="title-greeting">Have a nice day</p>
      </div>
      <div class="input-list mt-3">
        <form @submit.prevent="addTodo">
          <div class="mb-3">
            <div class="input-group">
              <input
                type="text"
                class="form-control"
                placeholder="Input your list"
                v-model="newTodo"
                required
              />
              <span class="input-group-btn">
                <button class="btn btn-primary" type="submit">
                  <i class="fa fa-plus"></i>
                </button>
              </span>
            </div>
          </div>
        </form>
      </div>
      <div class="title mt-3 text-center">
        <h4>Your todolist</h4>
      </div>
      <div class="mt-2">
        <div class="todo" v-for="todo in todos" :key="todo">
          <input
            type="checkbox"
            id="todo"
            name="todo"
            value="todo"
            v-model="todo.done"
            @click="toggleTodo(todo)"
          />
          <label for="todo" :class="{ done: todo.done }">{{
            todo.title
          }}</label>
          <label class="delete-todo" @click="deleteTodo(todo)"
            ><i class="fa fa-times"></i
          ></label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false,
      });
      this.newTodo = "";
      this.saveTodos();
    },
    deleteTodo(todo) {
      let todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
      this.saveTodos();
    },
    toggleTodo(todo) {
      todo.done = !todo.done;
      this.saveTodos();
    },
    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem("todo", parsed);
    },
  },
  mounted() {
    if (localStorage.getItem("todo")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todo"));
      } catch (e) {
        localStorage.removeItem("todo");
      }
    }
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap");
body {
  background-color: #1a1e6b;
}

.container {
  -webkit-box-pack: center;
      -ms-flex-pack: center;
          justify-content: center;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  padding: 20px;
  font-family: "Roboto", sans-serif;
  color: white;
}

input[type="checkbox"] {
  position: relative;
  width: 1em;
  height: 1em;
  color: #363839;
  border: 1px solid #bdc1c6;
  border-radius: 4px;
  -webkit-appearance: none;
     -moz-appearance: none;
          appearance: none;
  outline: 0;
  cursor: pointer;
  -webkit-transition: background 175ms cubic-bezier(0.1, 0.1, 0.25, 1);
  transition: background 175ms cubic-bezier(0.1, 0.1, 0.25, 1);
}

input[type="checkbox"]::before {
  position: absolute;
  content: "";
  display: block;
  left: 7px;
  width: 8px;
  height: 12px;
  border-style: solid;
  border-color: #fff;
  border-width: 0 2px 2px 0;
  -webkit-transform: rotate(45deg);
          transform: rotate(45deg);
  opacity: 0;
}

input[type="checkbox"]:checked {
  color: #fff;
  border-color: #00da41;
  background: #00da41;
}

input[type="checkbox"]:checked::before {
  opacity: 1;
}

input[type="checkbox"]:checked ~ label::before {
  -webkit-clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
          clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}

label {
  font-size: 17px;
  font-weight: 500;
  text-transform: capitalize;
  color: #a9ffa1;
  margin-left: 5px;
}

.done {
  text-decoration: line-through;
  color: #646464;
}

.delete-todo {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
}
/*# sourceMappingURL=style.css.map */
</style>