<script>
import draggable from "vuedraggable";
import TaskCard from "../components/TaskCard.vue";

export default {
  name: "App",
  components: {
    TaskCard,
    draggable
  },
  data() {
    return {
      columns : {
        col1: {
          tasks: [
            {
              id: 1,
              title: "Add discount code to checkout page",
            },
            {
              id: 2,
              title: "Provide documentation on integrations",
            },
            {
              id: 3,
              title: "Design shopping cart dropdown",
            },
          ]
        },
        col2: {
          tasks: [{
              id: 1,
              title: "Add discount code to checkout page",
            },
            {
              id: 2,
              title: "Provide documentation on integrations",
            },
            {
              id: 3,
              title: "Design shopping cart dropdown",
            },]
        }
      }
    };
  },

  methods: {

    // Save and get from Local Storage
    getFromLocalStorage() {
      localStorage.setItem('col', JSON.stringify(this.columns));
      const newColumns = JSON.parse(localStorage.getItem('col'));

      this.columns = newColumns;
    },

    // Add new Task
    addTask(col) {
      if (this.newTask !== "") {
        const newTaskObj = { id: 1, title: this.newTask };
        this.columns[col].tasks.push(newTaskObj);

        this.newTask = " ";
      }

      this.getFromLocalStorage();
    },

    // Add new Status Column 
    addStatus() {
      if (this.newStatus !== "") {
        this.columns[this.newStatus] = { tasks: [] };

        this.getFromLocalStorage();
      }

      this.newStatus = " ";
      console.log(this.columns);
    }
  }
};
</script>

<template>
  <div id="app">
    <div class="pt-10 pl-10">
      <!-- Add new Status Option -->
      <input 
        v-model="newStatus"
        class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        type="text" placeholder="Add new Status">
      <button 
        class=" bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 
        hover:border-blue-500 rounded mx-2 h-10" @click="addStatus">
        Add New
      </button>
    </div>

    <div class="flex justify-center relative">
      <div class="min-h-screen flex overflow-x-scroll py-12">
        <div v-for="key in Object.keys(columns)" :key="key"
          class="bg-gray-100 rounded-lg px-3 py-3 column-width rounded mr-4">
          <!-- Status Title -->
          <p class="text-gray-800 font-bold font-sans tracking-wide text-lg px-1 pb-2">
            {{ key }}
            <span class="text-red-500" style="float: right">{{columns[key].tasks.length}}</span>
          </p>

          <!-- Draggable component comes from vuedraggable. It provides drag & drop functionality -->
          <draggable :list="columns[key].tasks" :animation="200" ghost-class="ghost-card" group="tasks">

            <!-- Each element from here will be draggable and animated. Note :key is very important here to be unique both for draggable and animations to be smooth & consistent. -->
            <task-card v-for="(task) in columns[key].tasks" :key="task.id" :task="task" class="mt-3 cursor-move">
            </task-card>
          </draggable>

          <br />
          <input 
            v-model="newTask"
            class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            type="text" placeholder="Add new Task">
          <button 
            class=" bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 
            hover:border-blue-500 rounded mx-2 h-10" @click="addTask(key)">
            Add
          </button>

        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  column-width {
    min-width: 320px;
    width: 320px;
  }

  .ghost-card {
    opacity: 0.5;
    background: #F7FAFC;
    border: 1px solid #4299e1;
  }
</style>
