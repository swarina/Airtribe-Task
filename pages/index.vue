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
    addTask(col) {
      if (this.newTask !== "") {
        const newTaskObj = { id: 1, title: this.newTask };
        this.columns[col].tasks.push(newTaskObj);

        this.newTask = " ";
      }
    },

    newStatus() {

    }
  }
};
</script>

<template>
  <div id="app">
    <div class="flex justify-center">
      <div class="min-h-screen flex overflow-x-scroll py-12">
        <div v-for="key in Object.keys(columns)" :key="key"
          class="bg-gray-100 rounded-lg px-3 py-3 column-width rounded mr-4">
          <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">{{ key }}</p>
          
          <!-- Draggable component comes from vuedraggable. It provides drag & drop functionality -->
          <draggable :list="columns[key].tasks" :animation="200" ghost-class="ghost-card" group="tasks">
            
            <!-- Each element from here will be draggable and animated. Note :key is very important here to be unique both for draggable and animations to be smooth & consistent. -->
            <task-card v-for="(task) in columns[key].tasks" :key="task.id" :task="task" class="mt-3 cursor-move"></task-card>
            
          </draggable>
          
          <br />
          <input v-model="newTask" type="text">
          <button @click="addTask(key)">Add</button>
        </div>
        <!-- Add new Status Button -->
        <button @click="newStatus">Add New</button>
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
