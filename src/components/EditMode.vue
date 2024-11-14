<template>
    <div>
      <h2>Edit Mode for {{ part.title }}</h2>
      <button @click="addTopic">Add Topic</button>
      <div v-for="topic in part.topics" :key="topic.id">
        <h3>{{ topic.title }}</h3>
        <button @click="addTask(topic)">Add Task</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ["part"],
    methods: {
      addTopic() {
        const title = prompt("Enter topic title:");
        if (title) this.part.topics.push({ id: Date.now(), title, tasks: [] });
      },
      addTask(topic) {
        const question = prompt("Enter task question:");
        const answer = prompt("Enter task answer:");
        if (question && answer) topic.tasks.push({ question, answer });
      }
    }
  };
  </script>
  