<template>
  <div
      class="todo-container"
      :class="{
          done: checked,
          }"
  >
    <div>
    <input
      v-model="checked"
      type="checkbox"
  />
    </div>
    <input
       v-model="todo"
       class="todo-name"
       :disabled="checked"
    />
    <button
        class="btn-delete"
        @click="emitDeleteNote"
    >
      DELETE
    </button>
  </div>
</template>

<script>
import {toRefs} from "@vue/reactivity";

export default {
  name: "ToDo",
  props: {
    toDo: {
      type: Object,
      required: true,
    },
  },
  emits: ['deleteNote'],

  setup(props, {emit}) {

    const {checked, todo} = toRefs(props.toDo)

    const emitDeleteNote = () => {
      emit('deleteNote', props.toDo.id);
    };

    return {
      checked,
      todo,
      emitDeleteNote,
    }
  }
}
</script>

<style scoped>

input {
  outline: none;
}

.btn-delete {
  background-color: white;
  color: black;
  border: 2px solid black;
  border-radius: 4px;
}

.todo-name {
  font-size: 14px;
  border: 0px;
}

</style>
