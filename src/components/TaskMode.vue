<template>
    <div>
      <h2>Task Mode for {{ part.title }}</h2>
      <div v-if="currentTask">
        <p>{{ currentTask.question }}</p>
        <input type="text" v-model="userAnswer" />
        <button @click="submitAnswer">Submit</button>
      </div>
      <div v-else>
        <p>End of tasks. Correct answers: {{ correctCount }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ["part"],
    data() {
      return {
        currentTaskIndex: 0,
        userAnswer: "",
        correctCount: 0
      };
    },
    computed: {
      currentTask() {
        return this.part.tasks[this.currentTaskIndex];
      }
    },
    methods: {
      submitAnswer() {
        if (this.userAnswer === this.currentTask.answer) {
          this.correctCount++;
        }
        this.userAnswer = "";
        this.currentTaskIndex++;
      }
    }
  };
  </script>
  