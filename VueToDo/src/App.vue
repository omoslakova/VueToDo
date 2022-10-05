<template>
  <div class="wrapper">
    <h1 class="header"
    >
      ToDo List
    </h1>
    <div class="todo-input">
      <input
          v-model="newNoteName"
          type="text"
          placeholder="Add TO DO"
          @keypress.enter="addNewNote"
      />
    </div>
    <div class="add">
      <button class="btn-add"
              @click="addNewNote">
        ADD
      </button>
    </div>
    <div class="task">Task</div>
    <div class="action">Action</div>
    <div class="notes">
      <to-do
          v-for="(toDo) in notes"
          :key="toDo.id"
          :to-do="toDo"
          title="title"
          @deleteNote="removeNote"
      />
    </div>
  </div>
</template>

<script>

import ToDo from './components/ToDo.vue'
import {ref, onMounted} from 'vue';

export default {
  name: "App",
  components: {
    ToDo,
  },
  setup() {
    const newNoteName = ref('');
    const notes = ref([]);

    const addNewNote = () => {
      // todo add validation
      // todo max value reduce
      const newNote = {
        id: Math.max(...notes.value.map(notes => notes.id)) + 1,
        todo: newNoteName.value,
        checked: false
      }
      notes.value.push(newNote);
      newNoteName.value = ""
    };

    const removeNote = (id) => {
      const targetIndex = notes.value.findIndex((el) => el.id === id)
      notes.value.splice(targetIndex, 1)
    }

    onMounted(() => {
      fetch('https://dummyjson.com/todos')
          .then((res) => {
            return res.json();
          })
          .then((res) => {
            notes.value = res.todos
          })
    })

    return {
      notes,
      newNoteName,
      addNewNote,
      removeNote,
    };
  },
};

</script>

<style scoped>

.wrapper {
  font-family: Georgia;
  display: grid;
  grid-template-columns: 30px 30px 160px 100px auto;
  grid-template-rows: 80px 30px 30px auto;
  text-align: center;
}

.header {
  color: #2828b5;
  grid-column: 3 / 3;
  grid-row: 1 / 1;
}

.todo-input {
  grid-column: 2 / 3;
  grid-row: 2 / 2;
  align-items: center;
  outline: none;
}

.add {
  grid-column: 4 / 4;
  grid-row: 2 / 2;
  justify-self: start;
}

.btn-add {
  background-color: white;
  color: #2828b5;
  border: 2px solid #2828b5;
  border-radius: 4px;
}

.task {
  grid-column: 3 / 3;
  grid-row: 3 / 3;
  justify-self: start;
}

.action {
  grid-column: 4 / 4;
  grid-row: 3 / 3;
  justify-self: start;
}

.notes {
  grid-column: 1 / 4;
  grid-row: 4 / 4;
}

</style>
