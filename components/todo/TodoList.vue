<template>
  <section>
    <div class="todo-add_container">
      <b-collapse
        aria-id="addTodo"
        class="todo-add"
        v-model="isCreationOpen"
        animation="slide"
      >
        <div
          slot="trigger"
          role="button"
          aria-controls="addTodo"
          class="todo-add_title"
        >
          <strong>Ajouter une tache</strong>
        </div>
        <div class="todo-add_content">
          <b-field label="Titre">
            <b-input v-model="title" type="text" />
          </b-field>
          <b-field label="Description">
            <b-input v-model="description" type="text" />
          </b-field>
          <b-field label="Importance">
            <div class="todo-add_importance">
              <div>
                <input
                  type="radio"
                  v-model="importance"
                  id="yellow"
                  value="yellow"
                />
                <label for="yellow">
                  <span class="todo-add_importance--yellow"></span>
                </label>
              </div>
              <div>
                <input
                  type="radio"
                  v-model="importance"
                  id="orange"
                  value="orange"
                />
                <label for="orange">
                  <span class="todo-add_importance--orange"></span>
                </label>
              </div>
              <div>
                <input type="radio" v-model="importance" id="red" value="red" />
                <label for="red">
                  <span class="todo-add_importance--red"></span>
                </label>
              </div>
            </div>
          </b-field>
          <b-field label="Date">
             <b-datepicker
                v-model="date"
                :show-week-number="showWeekNumber"
                :locale="locale"
                placeholder="Cliquez pour sélectionner une date..."
                icon="calendar-today"
                trap-focus>
            </b-datepicker>
          </b-field>
          <b-button @click="addTodo" class="todo-add_button is-success" expanded
            >Ajouter</b-button
          >
        </div>
      </b-collapse>
    </div>
    <div class="card-container">
      <TodoItem
        @clicked="deleteTodo"
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
      ></TodoItem>
    </div>
  </section>
</template>

<script>
import TodoItem from "@/components/todo/TodoItem";
export default {
  name: "TodoList",
  components: {
    TodoItem
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Faire la vaisselle",
          description: "Je dois faire la vaisselle, c'est important",
          importance: "orange",
          completed: false
        },
        {
          id: 2,
          title: "Laver la SDB",
          description: "Je dois laver la SDB, c'est important",
          importance: "yellow",
          completed: false
        },
        {
          id: 2,
          title: "Finir la todo liste",
          description: "Je dois la finir rapidement",
          importance: "red",
          completed: false
        }
      ],
      title: "",
      description: "",
      importance: "",
      date: "",
      isCreationOpen: false
    };
  },
  methods: {
    addTodo() {
      if(this.title && this.description && this.importance) {
        this.todos.push({
          id: this.todos.length + 1,
          title: this.title,
          description: this.description,
          importance: this.importance
        });
      }
      else {
        console.log("error")
      }
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>

<style>
.todo-add {
  margin-top: 10px;
  border-radius: 5px;
  max-width: 500px;
}

.todo-add_title {
  padding: 15px;
  background-color: #dfdfdf;
}

.todo-add_content {
  padding: 20px;
  background-color: #f2f2f2;
}

.todo-add_button {
  margin-top: 30px;
}

.todo-add_importance {
  display: flex;
  justify-content: space-around;
}

.todo-add_importance input {
  display: none;
}

.todo-add_importance input:checked + label span {
  border: 2px solid #363636;
}

.todo-add_importance label span {
  width: 40px;
  height: 40px;
  display: inline-block;
  border-radius: 100%;
  cursor: pointer;
}

.todo-add_importance--yellow {
  background-color: #fff971;
}

.todo-add_importance--orange {
  background-color: #ff8b00;
}

.todo-add_importance--red {
  background-color: #ff0000;
}

.card-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-auto-columns: 300px;
  gap: 10px 10px;
  margin-top: 60px;
}
</style>
