<template>
  <div>
    <section id="task-list" class="w-1/2 mx-12">
      <ul class="m-auto justify-center">
        <li
          class="flex"
          @click="toggleCompeteHandler(i)"
          v-for="(task, i) in tasks"
          :key="i"
        >
          <CustomButton
            :index="i"
            @btnClicked="deleteTaskHandler(i)"
            buttonType="trash"
          />
          <span
            :class="['cursor-pointer ml-4', task.complete && 'line-through']"
          >
            {{ task.name }}
          </span>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
import CustomButton from "./uiElements/CustomButton.vue";

export default {
  name: "TaskList",
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    toggleCompeteHandler(i) {
      this.$emit("toggleComplete", i);
    },
    deleteTaskHandler(i) {
      console.log("delete", i);
      this.$emit("deleteEvent", i);
    },
  },
  components: {
    CustomButton,
  },
};
</script>

<style scoped></style>
