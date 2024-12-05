<template>
  <div id="app" class="container mt-5 text-center">
    <h1 class="mb-4">Тесты</h1>
    <div class="btn-group mb-4" role="group">
      <button class="btn btn-secondary" @click="selectApp('test1')">Найди пару эмодзи</button>
      <button class="btn btn-secondary" @click="selectApp('test2')">Путь стрелки</button>
      <button class="btn btn-secondary" @click="selectApp('test3')">Совпадает ли эмодзи?</button>
      <button class="btn btn-secondary" @click="selectApp('test4')">Тест 4</button>
      <button class="btn btn-secondary" @click="selectApp('test5')">Тест 5</button>
    </div>
    
    <div v-if="selectedApp == 'test1'">
      <Test1/>
    </div>
    <div v-else-if="selectedApp == 'test2'">
      <Test2/>
    </div>
    <div v-else-if="selectedApp == 'test3'">
      <Test3/>
    </div>
    <div v-else-if="selectedApp == 'test4'">

    </div>
    <div v-else-if="selectedApp == 'test5'">
      
    </div>
  </div>
</template>

<script>
import Test1 from './components/Test1.vue';
import Test2 from './components/Test2.vue';
import Test3 from './components/Test3.vue';

export default {
  components: {
    Test1,
    Test2,
    Test3
  },
  data() {
    return {
      selectedApp: null
    };
  },
  methods: {
    selectApp(app) {
      this.selectedApp = app;
    }
  }
};
</script>
