<template>
  <div class="wrapper">
    <div class="header">
      <h1>
      ToDo List
      </h1>
    </div>

    <div class="form">
      <input
          v-model="newNoteName"
          placeholder="Add TO DO"
          @keypress.enter="addNewNote"
      />
      <button
          class="form__btn-add"
          @click="addNewNote">
        ADD
      </button>
    </div>

    <div class="notes">
      <div class="notes__row notes__row_header">
        <div></div>
        <div class="task">Task</div>
        <div class="action">Action</div>
      </div>
      <to-do
            v-for="(toDo) in notes"
            :key="toDo.id"
            :to-do="toDo"
            class="notes__row"
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
  text-align: center;
  width: 400px;
}

.header {
  color: #2828b5;
}

.form {
  align-items: center;
  outline: none;
  position: relative;
  padding-bottom: 20px;
}

.form__btn-add {
  background-color: white;
  color: #2828b5;
  border: 2px solid #2828b5;
  border-radius: 4px;
  width: 80px;
  position: absolute;
  left: 320px;
}

.notes {
  position: relative;
}
.notes__row {
  display: grid;
  grid-template-columns: 30px 1fr 80px;
  grid-gap: 10px;
}

</style>
