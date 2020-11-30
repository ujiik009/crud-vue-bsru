<template>
  <div>
    <div class="task">
      <h3>{{ item.name }} {{ column_index }} {{ task_index }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: Object,
    column_index: Number,
    task_index: Number,
  }
};
</script>

<style>
.task {
  width: auto;
  border-radius: 10px;
  height: 100px;
  background-color: #72b6e0;
  margin: 10px;
}
</style>