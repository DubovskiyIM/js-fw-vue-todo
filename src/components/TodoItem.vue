<template>
  <li>{{idx + 1}}: {{todo}} </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: String,
      required: true
    },
    idx: {
      type: Number,
      required: true
    }
  }
};
</script>

<style scoped>

</style>
