<template>
  <div class="todo-list">
    <h1>Minha Lista de Tarefas</h1>
    <input
      v-model="newTask"
      @keyup.enter="addTask"
      placeholder="Digite uma nova tarefa e pressione Enter"
    />
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input
          type="checkbox"
          v-model="task.completed"
        />
        {{ task.text }}
        <button @click="removeTask(task.id)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === '') return;
      this.tasks.push({
        id: Date.now(),
        text: this.newTask,
        completed: false
      });
      this.newTask = '';
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    }
  }
};
</script>

<style scoped>
.todo-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 1em;
  border: 1px solid #f0a6b3;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #fce4ec;
}

h1 {
  color: #ec407a;
  font-size: 2em;
  margin-bottom: 1em;
}

input[type="text"] {
  width: calc(100% - 110px);
  padding: 0.5em;
  border-radius: 4px;
  border: 1px solid #ec407a;
  margin-bottom: 1em;
}

button {
  background-color: #ec407a; 
  color: white;
  border: none;
  border-radius: 4px;
  padding: 0.5em 1em;
  cursor: pointer;
  margin-left: 1em;
}


button:hover {
  background-color: #d81b60;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  padding: 0.5em 0;
  border-bottom: 1px solid #f0a6b3;
}

input[type="checkbox"] {
  margin-right: 0.5em;
}

span {
  flex: 1;
}
</style>
