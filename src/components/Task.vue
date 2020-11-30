<template>
  <div>
    <div class="task" draggable>
      <h3>{{ item.name }} {{ column_index }} {{ item_index }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: Object,
    column_index: Number,
    item_index: Number,
  },
  methods: {
    dragstart() {
      console.log("dragstart");
    },
  },
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