<template>
  <div class="w-full">
    <section id="input-area" class="m-auto w-1/2 px-8">
      <h1 class="text-2xl text-center font-semibold">
        {{ taskCount }} {{ taskCount === 1 ? "Task" : "Tasks" }}
      </h1>

      <form @submit.prevent>
        <input
          :placeholder="'Add Task # ' + (tasks.length + 1)"
          class="border-2 border-black rounded-md w-full px-2 text-center"
          type="text"
          v-model="newTask"
        />
        <button
          @click="addTaskHandler"
          class="border-2 border-black rounded-md hidden"
        >
          Add Task
        </button>
      </form>
    </section>
    <TaskList
      v-show="tasks.length"
      @deleteEvent="deleteEventHandler"
      @toggleComplete="toggleCompleteHandler"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue";

export default {
  name: "App",
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    deleteEventHandler(i) {
      this.tasks.splice(i, 1);
    },
    toggleCompleteHandler(i) {
      if (this.tasks.length < 1) return;
      const currentTaskCompleteStatus = this.tasks[i].complete;
      const newCompleteValue = !currentTaskCompleteStatus;

      this.tasks[i].complete = newCompleteValue;
    },
    addTaskHandler() {
      if (!this.newTask) return;

      this.tasks.push(this.newTaskObject);
      this.newTask = "";
    },
  },
  computed: {
    taskCount() {
      return this.tasks.length;
    },
    newTaskObject() {
      return {
        id: this.tasks.length + 1,
        name: this.newTask,
        complete: false,
      };
    },
  },
  components: {
    TaskList,
  },
};
</script>

<style></style>
