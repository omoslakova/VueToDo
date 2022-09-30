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
}

</script>

<template>
  <div class="todo">
    {{toDo.name}}
  </div>
</template>


<style scoped>
.read-the-docs {
  color: #888;
}

.li {
  list-style-type: none;
}
</style>
