<template>
  <div class="container text-center">
    <div v-if="!gameOver">
      <div class="text-center p-5 rounded mb-4">
        <h1 class="display-1">{{ currentEmoji }}</h1>
      </div>
      <div v-if="generateButtons" class="d-flex justify-content-center mb-3">
        <button class="btn btn-primary mx-2" @click="checkAnswer(true)">Да</button>
        <button class="btn btn-primary mx-2" @click="checkAnswer(false)">Нет</button>
      </div>
      <div class="my-2">Счет: {{ score }}</div>
      <div class="my-2">Осталось {{ time }} секунд</div>
    </div>
    <div v-else>
      <h2>Игра окончена, Счет: {{ score }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      emojiList: ['😀', '😃', '😄', '😆'],
      currentEmoji: '',
      previousEmoji: '',
      score: 0,
      time: 60,
      timer: null,
      gameOver: false,
      generateButtons: false
    };
  },
  methods: {
    generateNewEmoji() {
      this.previousEmoji = this.currentEmoji; 
      this.currentEmoji = this.emojiList[Math.floor(Math.random() * this.emojiList.length)];
    },
    checkAnswer(answer) {
      const isEqual = this.currentEmoji === this.previousEmoji;

      if ((isEqual && answer) || (!isEqual && !answer)) {
        this.score++;
      } else {
        this.score -= 3;
      }

      this.generateNewEmoji(); 
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.time--;
        if (this.time <= 0) {
          this.stopGame();
        }
      }, 1000);
    },
    stopGame() {
      this.gameOver = true;
      clearInterval(this.timer);
    }
  },
  mounted() {
    this.generateNewEmoji();
    setTimeout(() => {
      this.startTimer();
      this.generateButtons = true;
      this.generateNewEmoji(); 
    }, 3000);
  }
};
</script>