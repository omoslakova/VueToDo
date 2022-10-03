<template>
  <h1>ToDo List</h1>
  <div>
    <input
        type="text"
        v-model="newNoteName"
        placeholder="Add TO DO"
        @keypress.enter="addNewNote"
    />
    <button @click="addNewNote">
      ADD
    </button>
  </div>
  <div>Task</div>
  <div>Action</div>
  <div v-for="(toDo, index) in notes">
    <to-do
        :key="toDo.id"
        :to-do="toDo"
    />
    <button @click="removeNote">
      DELETE
    </button>
  </div>
</template>


<script>
import ToDo from './components/ToDo.vue'
import { ref } from 'vue';

export default {
  name: "App",
  components: {
    ToDo,
  },
  setup() {
    const newNoteName = ref('');
    const notes = ref([
      {
        id: 1,
        name: "note1",
        checked: false
      },
      {
        id: 2,
        name: "note2",
        checked: false
      },
      {
        id: 3,
        name: "note3",
        checked: false
      }
    ]);

    const addNewNote = () => {
      // todo add validation
      // todo max value reduce
      const newNote = ref({
        id: 4 + 1,
        name: newNoteName.value,
        checked: false
      })
      notes.value.push(newNote.value)
    };

    const removeNote = (index) => {
      notes.value.splice(index, 1)
    }

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
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
