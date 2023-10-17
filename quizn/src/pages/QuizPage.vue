<template>
  <div class="quiz">
    <h1>{{ quizTitle }}</h1>
    <div v-if="quizCompleted">
      <p v-if="score === quizQuestions.length">Вы прошли на максимальный бал</p>
      <p v-else-if="score === 0">Вы прошли на ноль баллов</p>
      <p v-else-if="score < quizQuestions.length">Вы почти молодец</p>
    </div>
    <div v-else>
      <div v-if="currentQuestionIndex < quizQuestions.length" class="question-container">
        <h2>{{ quizQuestions[currentQuestionIndex].question }}</h2>
        <ul>
          <li v-for="(option, optionIndex) in quizQuestions[currentQuestionIndex].options" :key="optionIndex">
            <label>
              <input
                type="radio"
                :name="'question-' + currentQuestionIndex"
                :value="option"
                v-model="selectedAnswers[currentQuestionIndex]"
              />
              {{ option }}
            </label>
          </li>
        </ul>
        <button class="btn" @click="NextQuest">Следующий вопрос</button>
      </div>
      <div v-else>
        <button class="btn" @click="checkAnswers">Завершить тест</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quizTitle: "Моя викторина",
      quizQuestions: [
        {
          question: "Какой тег используется для создания ссылок на другие веб-страницы?",
          options: ["<a>", "<img>", "<div>"],
          correctAnswer: "<a>"
        },
        {
          question: "Какой атрибут HTML используется для задания названия веб-страницы?",
          options: ["title", "name", "id"],
          correctAnswer: "title"
        },
        {
          question: "Какой язык программирования используется для создания динамических веб-страниц?",
          options: ["C++", "JavaScript", "C#"],
          correctAnswer: "JavaScript"
        },
        {
          question: "Какой элемент HTML используется для создания таблиц на веб-страницах?",
          options: ["<table>", "<form>", "<ul>"],
          correctAnswer: "<table>"
        },
        {
          question: "Какое свойство CSS используется для задания размера шрифта текста?",
          options: ["font-size", "text-size", "font-style"],
          correctAnswer: "font-size"
        },
        // Добавьте остальные вопросы
      ],
      selectedAnswers: [],
      quizCompleted: false,
      score: 0,
      currentQuestionIndex: 0
    };
  },
  methods: {
    nextQuestionAnimation() {
      const questionContainer = document.querySelector('.question-container');
      questionContainer.classList.remove('question-container');
      void questionContainer.offsetWidth;
      questionContainer.classList.add('question-container');
    },
    NextQuest() {
      if (this.selectedAnswers[this.currentQuestionIndex] === undefined) {
        alert("Пожалуйста, выберите ответ на текущий вопрос");
        return;
      }
      this.currentQuestionIndex++;
      this.nextQuestionAnimation();
    },
    checkAnswers() {
      this.score = 0;
      for (let i = 0; i < this.quizQuestions.length; i++) {
        if (this.selectedAnswers[i] === this.quizQuestions[i].correctAnswer) {
          this.score++;
        }
      }
      this.quizCompleted = true;
    }
  }
};
</script>

<style scoped>
.quiz {
  max-width: auto;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(to bottom, grey, #f2f2f2);
  margin:auto;
}
.question-container {
  animation: slideInRight 0.78s ease-in-out;
}

@keyframes slideInRight {
  0% {
    transform: translateX(100%);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
.btn{
text-decoration: none;
  background-color: transparent;
  border: 3px solid;
  border-radius: 20px;
  width: 220px; 
  height: 60px;
  font-size: 20px;
  margin: 1em;
  transition: color 1s, border-color 1s;

  color:black;
}
.btn:hover{
  
  border-color: red;
}
</style>