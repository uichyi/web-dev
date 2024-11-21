<template>
    <div class="container mt-4">
      <div class="mb-3">
        <input v-model="newTodoDescription" placeholder="Описание дела" class="form-control" />
        <button @click="addTodo" class="btn btn-primary mt-2">Добавить дело</button>
      </div>
      <table class="table">
        <thead>
          <tr>
            <th>№</th>
            <th>Описание</th>
            <th>Статус</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in todos" :key="todo.id" :style="statusStyle(todo.status)">
            <td>{{ todo.id }}</td>
            <td>{{ todo.description }}</td>
            <td>
              <select v-model="todo.status">
                <option value="Не в работе">Не в работе</option>
                <option value="В работе">В работе</option>
                <option value="Выполнено">Выполнено</option>
                <option value="Отменено">Отменено</option>
              </select>
            </td>
            <td>
              <button class="btn btn-danger" @click="deleteTodo(todo.id)">Удалить</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        todos: [],
        newTodoDescription: '',
        nextId: 1,
      };
    },
    methods: {
      addTodo() {
        if (this.newTodoDescription.trim() == '') return;
        
        this.todos.push({
          id: this.nextId++,
          description: this.newTodoDescription,
          status: 'Не в работе'
        });
        this.newTodoDescription = '';
      },
      deleteTodo(id) {
        this.todos = this.todos.filter(todo => todo.id != id);
      },
      statusStyle(status) {
        switch (status) {
          case 'Выполнено':
            return { color: 'lightgreen' };
          case 'Отменено':
            return { color: 'red' };
          case 'В работе':
            return { color: 'blue' };
          default:
            return {};
        }
      },
    },
  };
  </script>