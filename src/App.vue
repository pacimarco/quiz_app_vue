<template>
  <div class="quiz">
    <h1 class="title">Quiz</h1>
    <div v-if="!completed">
      <div  v-for="(question, index) in questions" :key="index">
        <h2 class="questione">{{ question.question }}</h2>
        <div class="options">
          <div v-for="(option, optionIndex) in question.options" :key="optionIndex" class="option">
            <label>
              <input type="radio" :name="'question-' + index" :value="optionIndex" v-model="selected[index]" @change="SetAnswer">
              <span class="option-text">{{ option }}</span>
            </label>
          </div>
        </div>
      </div>
      <button class="submit-button" @click="checkAnswers">Submit</button>
    </div>
    <div v-if="completed">
      <h2 class="score">Your score is {{ score }}/{{ questions.length }}</h2>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      questions: [
        {
          question: 'What is the capital of Italy?',
          options: ['Milan', 'Rome', 'Naples', 'Turin'],
          answer: 1
        },
        {
          question: 'What is the highest mountain in the world?',
          options: ['Mount Kilimanjaro', 'Mount Everest', 'Mount Fuji', 'Mount Denali'],
          answer: 1
        },
        {
          question: 'What is the smallest country in the world?',
          options: ['Monaco', 'Vatican City', 'San Marino', 'Liechtenstein'],
          answer: 1
        }
      ],
      selected: [],
      completed: false
    }
  },
  computed: {
    score() {
      let correct = 0
      for (let i = 0; i < this.questions.length; i++) {
        if (this.selected[i] === this.questions[i].answer) {
          correct++
        }
      }
      return correct
    }
  },
  methods: {
    checkAnswers() {
      this.completed = true
    }
  }
}
</script>


<style lang="scss">

$primary-color: #007bff;

body {
  margin: 0;
  font-family: Arial, sans-serif;
  font-size: 16px;
  line-height: 1.5;
  background-color: #271C36;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}

h1 {
  margin-top: 0;
  margin-bottom: 20px;
  font-size: 32px;
  font-weight: bold;
  color: $primary-color;
}

.questione {
      
      color: yellow;
    }

.quiz {
  margin-top: 40px;
}

    

    .score {
      color: yellow;
    }
  

  .submit-button{
    background-color: yellow;
  }

  .options {
    display: flex;
    flex-direction: column;

    .option {
      display: block;
      margin-bottom: 10px;
      padding: 10px;
      border-radius: 5px;
      background-color: #d82323;
      cursor: pointer;
      transition: background-color 0.2s ease-in-out;

      &:hover {
        background-color: yellow;
      }

      &.correct {
        background-color: #d4edda;
      }

      &.wrong {
        background-color: #f8d7da;
      }

      input[type="radio"] {
        margin-right: 10px;
        cursor: pointer;
      }
    }
  }



</style>
