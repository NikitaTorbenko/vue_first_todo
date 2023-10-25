<script>
import TaskCard from './components/TaskCard.vue';
import TaskInput from './components/TaskInput.vue';
import { ref } from 'vue';

export default {
  components: {
    TaskCard,
    TaskInput,
  },
  setup() {
    const taskList = ref([
      {
        id: 0,
        title: 'Написать тудуху',
        description: 'нгрукащуоцв',
        status: false,
      },
    ]);

    const addTask = ({ title, description }) => {
      taskList.value = [
        ...taskList.value,
        {
          id: taskList.value[taskList.value.length - 1].id + 1,
          title,
          description,
          status: false,
        },
      ];
    };

    const setDoneTask = id => {
      taskList.value = taskList.value.map(x => {
        if (x.id === id) x.status = true;
        return x;
      });
    };
    const removeTask = id => {
      taskList.value = taskList.value.filter(x => x.id !== id);
    };

    return {
      taskList,
      addTask,
      removeTask,
      setDoneTask,
    };
  },
};
</script>

<template>
  <main>
    <TaskInput @onAddTask="addTask" />
    <ul class="task-list my-list">
      <li v-for="item in taskList" :key="item.id">
        <TaskCard
          @onDone="setDoneTask(item.id)"
          @onRemove="removeTask(item.id)"
          :model="item"
        />
      </li>
    </ul>
  </main>
</template>
<style lang="scss">
* {
  font-family: serif;
  margin: 0;
  padding: 0;
}

main {
  min-width: 450px;
  margin: 0 auto;
  width: 100%;
  max-width: 900px;
  margin-top: 50px;
}

button,
input,
.my-style {
  border-radius: 5px;
  border: 1px solid lightgray;
  padding: 10px;
}

.my-list {
  display: grid;
  grid-template-rows: auto;
  grid-template-columns: 100%;
  grid-gap: 5px;
}

.task-list {
  list-style: none;
}
</style>
