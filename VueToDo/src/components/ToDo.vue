<template>
  <div class="todo">
    {{toDo.name}}
  </div>
</template>

<script>
import {ref} from 'vue'

export default {
  name: "ToDo",
  props: {
    toDo: {
      type: Object,
      required: true,
    },
  },
  setup() {
    return {
    }
  }
}

</script>




<style scoped>
.read-the-docs {
  color: #888;
}

.li {
  list-style-type: none;
}
</style>
