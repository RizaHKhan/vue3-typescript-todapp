<template>
  <form @submit.prevent="addItem($event)">
    <label for="title">Title</label>
    <input type="text" name="title" placeholder="Enter Task Title" required />

    <label for="completed">Completed</label>
    <select name="completed" required>
      <option value="true">True</option>
      <option value="false" selected>False</option>
    </select>

    <input class="button" type="submit" value="Create Item" />
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Form",
  setup(props, { emit }) {
    const addItem = (e: any) => {
      const task: any = {};
      for (const elements of e.target.elements) {
        if (elements.name) {
          if (elements.name === "completed") {
            task[elements.name] = elements.value === "true" ? true : false;
          } else {
            task[elements.name] = elements.value;
          }
          elements.value = "";
        }
      }
      emit("new-task", task);
    };

    return { addItem };
  },
});
</script>
