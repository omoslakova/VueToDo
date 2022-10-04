<template>
  <div
      class="todo"
      :class="{
          done: checked,
          }"
  >
    <input
      v-model="checked"
      type="checkbox"
  />
    <input
       v-model="name"
       :disabled="checked"
    />
    <button @click="emitDeleteNote"
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

    const {checked, name} = toRefs(props.toDo)

    const emitDeleteNote = () => {
      emit('deleteNote', props.toDo.id);
    };

    return {
      checked,
      name,
      emitDeleteNote,

    }
  }
}

</script>


<style scoped>
.done {
  color: gray;
}
</style>
