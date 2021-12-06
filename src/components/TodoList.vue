<template>
  <div id="app">
    <h1>Todoリスト</h1>
    <form>
      <input type="radio" name="status" id="all" checked @change="filterAll" />
      <label for="all">すべて</label>
      <input type="radio" name="status" id="working" @change="filterWorking" />
      <label for="working">作業中</label>
      <input
        type="radio"
        name="status"
        id="complete"
        @change="filterComplete"
      />
      <label for="complete">完了</label>
    </form>
    <br />
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>コメント</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in fileterTodos" :key="todo.newTodo_id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.newTodo }}</td>
          <td>
            <button @click="changeStatus(index)">{{ todo.status }}</button>
          </td>
          <td><button @click="deleteTodo(index)">削除</button></td>
        </tr>
      </tbody>
    </table>
    <h1>新規タスクの追加</h1>
    <input type="text" v-model="newTodo" />
    <button id="addTask" @click="addTodo">追加</button>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      newTodo: "",
      todos: [],
      filterStatus: "",
    };
  },
  computed: {
    fileterTodos() {
      if (this.filterStatus === "") {
        return this.todos;
      } else {
        return this.todos.filter((todo) => todo.status === this.filterStatus);
      }
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo === "") return;
      const todo = {
        id: this.todos.length,
        newTodo: this.newTodo,
        status: "作業中",
      };
      this.todos.push(todo);
      this.newTodo = "";
    },
    changeStatus(index) {
      if (this.fileterTodos[index].status === "作業中") {
        this.fileterTodos[index].status = "完了";
      } else {
        this.fileterTodos[index].status = "作業中";
      }
    },
    deleteTodo(target) {
      this.todos.splice(target, 1);
      this.todos.forEach((todo, index) => {
        todo.id = index;
      });
    },
    filterAll() {
      this.filterStatus = "";
    },
    filterWorking() {
      this.filterStatus = "作業中";
    },
    filterComplete() {
      this.filterStatus = "完了";
    },
  },
};
</script>
