<template>
  <div>
    <div class="card">
      <header class="card-header">
        <p class="card-header-title">
          {{ todo.title }}
        </p>
        <span
          class="card-header-importance"
          :importance="todo.importance"
        ></span>
      </header>
      <div class="card-content">
        <div class="content">
          {{ todo.description }}
          <br />
          <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
        </div>
      </div>
      <footer class="card-footer">
        <b-button type="is-info is-light" class="card-footer-item"
          >Edit</b-button
        >
        <b-button
          @click="deleteTodo"
          type="is-danger is-light"
          class="card-footer-item"
          >Delete</b-button
        >
      </footer>
    </div>
  </div>
</template>

<script>



export default {
  name: "TodoItem",
  props: {
    todo: Object
  },
  methods: {
    deleteTodo(event) {
      console.log(this.todo.id);
      this.$emit("clicked", this.todo.id);
    }
  }
};
</script>

<style>
.card-header span[importance="yellow"] {
  background-color: #fff971;
}
.card-header span[importance="orange"] {
  background-color: #ff8b00;
}
.card-header span[importance="red"] {
  background-color: #ff0000;
}

.card-header {
  display: flex;
  align-items: center;
  
}
.card-header span {
  width: 20px;
  height: 20px;
  border-radius: 100%;
  margin-right:20px
}
</style>
