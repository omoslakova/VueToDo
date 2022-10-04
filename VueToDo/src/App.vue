<template>
  <h1>ToDo List</h1>
  <div>
    <input
        v-model="newNoteName"
        type="text"
        placeholder="Add TO DO"
        @keypress.enter="addNewNote"
    />
    <button @click="addNewNote">
      ADD
    </button>
  </div>
  <div>
  <div>Task</div>
  <div>Action</div>
  <div>
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
      const newNote = {
        id: Math.max(...notes.value.map(notes => notes.id)) + 1,
        name: newNoteName.value,
        checked: false
      }
      notes.value.push(newNote);
      newNoteName.value = ""
    };

    const removeNote = (id) => {
      const targetIndex = notes.value.findIndex( (el) => el.id === id)
      notes.value.splice(targetIndex, 1)
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

</style>
