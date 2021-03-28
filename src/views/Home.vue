<template>
  <div class="home">
    <Form @new-task="addItem" />
    <table>
      <tr>
        <th>Title</th>
        <th>Completed</th>
        <th>Toggle State</th>
      </tr>
      <tr v-for="({ title, completed }, i) in list" :key="title">
        <td>{{ title }}</td>
        <td>{{ completed }}</td>
        <td><button @click="toggleCompleted(i)">Change State</button></td>
      </tr>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Form from "@/components/Form.vue";

interface Task {
  title: string;
  completed: boolean;
}

export default defineComponent({
  name: "Home",
  components: {
    Form,
  },
  setup() {
    const list = ref<Task[]>([]);

    const addItem = (item: any) => {
      list.value.push(item);
    };

    const toggleCompleted = (index: number) => {
      list.value[index].completed = !list.value[index].completed;
    };

    return { list, addItem, toggleCompleted };
  },
});
</script>

<style lang="scss">
form {
  display: flex;
  flex-direction: column;
  max-width: 300px;
  margin: 10px 0;

  label {
    margin: 0.5rem 0;
  }

  input {
    margin: 0.5rem 0;
    border: 0;
    border-bottom: 1px solid black;
    padding: 0.5rem 1rem;
  }
  .button {
    border: 0;
    border-radius: 5px;
    padding: 0.5rem 1rem;
  }
}
td {
  border-bottom: solid 1px rgba(0, 0, 0, 0.2);
  width: 300px;
}
</style>
