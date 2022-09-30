<script>
import ToDo from './components/ToDo.vue'

export default {
  name: "App",
  components: {
    ToDo,
  },
  data() {
    return {
      placeholderString: 'Add TO DO',
      newNoteName: '',
      notes: [
        {id: 1, name: "note1", checked: true},
        {id: 2, name: "note2", checked: true},
        {id: 3, name: "note3", checked: true}
      ]
    }
  },
  methods: {
    addNewNote() {
      if (this.inputValue !== '') {
        this.notes.push(this.inputValue)
        this.inputValue = ''
      }
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  },
  changeNote: function (index) {
  },
}
</script>

<template>
  <h1>ToDo List</h1>
  <div>
    <input
        type="text"
        placeholder="Add TO DO">
    <button
        @click="addNewNote">ADD
    </button>
  </div>
  <div>Task</div>
  <div>Action</div>
  <to-do
      v-for="(toDo) in notes"
      :key="toDo.id"
      :to-do="toDo"
  />
</template>



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
