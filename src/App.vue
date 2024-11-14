<template>
  <div>
    <div v-if="!isAuthenticated">
      <h2>Enter Password to Access Content</h2>
      <input type="password" v-model="enteredPassword" placeholder="Enter password" />
      <button @click="checkPassword">Submit</button>
      <p v-if="errorMessage">{{ errorMessage }}</p>
    </div>

    <div v-else class="app-container">
      <Sidebar :subjects="subjects" @selectSubject="selectSubject" @loadData="loadDataFromFile" />
      <main class="main-content">
        <ResourceManager v-if="selectedSubject" :subject="selectedSubject" />
      </main>
    </div>
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar.vue";
import ResourceManager from "./components/ResourceManager.vue";

export default {
  data() {
    return {
      enteredPassword: "",
      correctPassword: "12345",
      isAuthenticated: false,
      errorMessage: "",
      subjects: ["Math", "Science", "History"], // Example subjects
      selectedSubject: null
    };
  },
  methods: {
    checkPassword() {
      if (this.enteredPassword === this.correctPassword) {
        this.isAuthenticated = true;
        this.errorMessage = "";
      } else {
        this.errorMessage = "Incorrect password. Please try again.";
      }
    },
    selectSubject(subject) {
      this.selectedSubject = subject;
    },
    loadDataFromFile(subjects) {
      this.subjects = subjects;
    }
  }
};
</script>
