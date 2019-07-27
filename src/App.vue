<template>
  <div id="app">
    <vue-flip width="100%" height="80%" :bindWithMe="flipped">
      <div slot="front" class="question_container" @click="flipped = true">
        <h1 class="question">{{ selectedQuestion.question }}</h1>
      </div>
      <div slot="back" class="answer_container" @click="flipped = false">
        <h2 class="answer">{{ selectedQuestion.answer }}</h2>
      </div>
    </vue-flip>
    <button class="nextQuestion" @click="nextQuestion">Next</button>
  </div>
</template>

<script>
import questions from './data/questions.json';
import VueFlip from 'vue-flip';

export default {
  name: 'app',
  components: {
    VueFlip
  },
  data() {
    return {
      questions: questions,
      selectedQuestion: null,
      flipped: false
    }
  },
  methods: {
    /**
     * Get the next question for the notecards and flip the card back to question side
     */
    nextQuestion() {
      this.flipped = false; 
      const newQuestion = this.questions[Math.floor(Math.random() * this.questions.length)];
      this.selectedQuestion = newQuestion;
    }
  },
  created () {
    /**
     * Get the first question on load
     */
    this.nextQuestion();
  },
}
</script>

<style>
html {
  height: 100%;
  width: 100%;
  margin: 0;
}

body {
  background: #090821;
  height: 100%;
  width: 100%;
  margin: 0;
  position: absolute;
  top: 0;
}

#app {
  padding: 10%;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  height: 100%;
  box-sizing: border-box;
}

.front, .back {
  height: 300px;
  padding: 20px;
  box-sizing: border-box;
  text-align: center;
  background:#2d3058;
  color: white;
}

.front {
  z-index: 1;
  font-size: inherit;
  font-family: inherit;
  padding: 0.5em 1em;
  outline: none;
  border: none;
}

.front:hover {
  cursor: pointer;
  animation: jelly 0.5s;
}

@keyframes jelly {
  0%,
  100% {
    transform: scale(1, 1);
  }
  25% {
    transform: scale(0.9, 1.1);
  }
  50% {
    transform: scale(1.1, 0.9);
  }
  75% {
    transform: scale(0.95, 1.05);
  }
}

.question_container, .answer_container {
  height: 90%;
  vertical-align: middle;
  overflow: auto;
}

.question, .answer {
  width: 95%;
  margin: 20px 0;
}

.nextQuestion {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 65px;
  font-family:sans-serif;
  font-size: 20px; 
  font-weight: bold;
  z-index: 1;
  color: #2d3058;
  padding: 0.5em 1em;
  outline: none;
  border: none;
}

.nextQuestion::before {
  content: '';
  z-index: -1;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: slategray;
  transform-origin: center top;
  transform: scaleY(0);
  transition: transform 0.25s ease-in-out;
}

.nextQuestion:hover {
  cursor: pointer;
  color: white;
}

.nextQuestion:hover::before {
  transform-origin: center bottom;
  transform: scaleY(1);
}

::-webkit-scrollbar {
  width: 1em;
}
 
::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
  border-radius: 10px;
}
 
::-webkit-scrollbar-thumb {
  background-color: lightgrey;
  outline: 1px solid slategrey;
  border-radius: 10px;
}

@media (max-width:480px) {
  .question {
    font-size: 1.5em;
  }
}

</style>
