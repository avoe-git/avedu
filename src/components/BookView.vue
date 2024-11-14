<template>
    <div>
      <h2>{{ book.title }}</h2>
      <button @click="addPart">Add Part</button>
      <div v-for="part in parts" :key="part.id">
        <h3 @click="selectPart(part)">{{ part.title }}</h3>
      </div>
  
      <EditMode v-if="selectedPart && editMode" :part="selectedPart" />
      <TaskMode v-else-if="selectedPart && !editMode" :part="selectedPart" />
      <button @click="toggleMode">Toggle Mode</button>
    </div>
  </template>
  
  <script>
  import EditMode from "./EditMode.vue";
  import TaskMode from "./TaskMode.vue";
  
  export default {
    props: ["book"],
    data() {
      return {
        parts: [],
        selectedPart: null,
        editMode: true
      };
    },
    methods: {
      addPart() {
        const title = prompt("Enter part title:");
        if (title) this.parts.push({ id: Date.now(), title, topics: [] });
      },
      selectPart(part) {
        this.selectedPart = part;
      },
      toggleMode() {
        this.editMode = !this.editMode;
      }
    },
    components: {
      EditMode,
      TaskMode
    }
  };
  </script>
  