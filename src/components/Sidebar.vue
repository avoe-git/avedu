<template>
    <div class="sidebar">
      <h2>Subjects</h2>
      <ul>
        <li v-for="subject in subjects" :key="subject" @click="selectSubject(subject)">
          {{ subject }}
        </li>
      </ul>
      <div class="actions">
        <button @click="exportData">Export Data</button>
        <input type="file" @change="loadData" accept=".avoe" />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ["subjects"],
    methods: {
      selectSubject(subject) {
        this.$emit("selectSubject", subject);
      },
      exportData() {
        const data = JSON.stringify({ subjects: this.subjects });
        const blob = new Blob([data], { type: "application/json" });
        const link = document.createElement("a");
        link.href = URL.createObjectURL(blob);
        link.download = "username.avoe"; // Modify username dynamically if needed
        link.click();
      },
      loadData(event) {
        const file = event.target.files[0];
        if (file && file.name.endsWith(".avoe")) {
          const reader = new FileReader();
          reader.onload = (e) => {
            try {
              const data = JSON.parse(e.target.result);
              this.$emit("loadData", data.subjects);
            } catch (error) {
              alert("Error loading file data.");
            }
          };
          reader.readAsText(file);
        } else {
          alert("Please upload a valid .avoe file.");
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .sidebar {
    width: 200px;
    background-color: #f4f4f4;
    padding: 10px;
  }
  .sidebar ul {
    list-style-type: none;
    padding: 0;
  }
  .sidebar li {
    cursor: pointer;
    padding: 5px;
  }
  .actions {
    margin-top: 10px;
  }
  </style>
  