<template>
  <q-page class="quiz-page">
    <q-card class="quiz-card">
      <q-card-section class="quiz-card-section">
        <h2 class="quiz-title">Добро пожаловать в наш Quiz!</h2>
        <p class="quiz-description">Пройдите наш тест и проверьте свои знания.</p>
        <q-btn class="quiz-start-btn" @click="startQuiz">Начать тест</q-btn>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  methods: {
    startQuiz() {
      // переход на страницу с тестом
      this.$router.push('/quiz');
    }
  }
}
</script>

<style>
.quiz-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.quiz-card {
  max-width: 500px;
  width: 100%;
}

.quiz-card-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.quiz-title {
  font-size: 2rem;
  margin-bottom: 20px;
}

.quiz-description {
  font-size: 1.2rem;
  margin-bottom: 40px;
}

.quiz-start-btn {
  font-size: 1.2rem;
  padding: 10px 20px;
}
</style>
