<template>
  <div>
    <slot></slot>
    <div class="task" draggable @dragstart="$emit('dragstart')">
      <div class="task_name">{{ item.name }}</div>

      <div class="state_display">
        {{ item.created_at }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: Object,
    column_index: Number,
    task_index: Number,
  },
};
</script>

<style>
.task_name {
  font-size: 20px;
  padding: 5px;
  font-weight: bold;
}
.task {
  position: relative;
  width: auto;
  border-radius: 2px;
  height: 100px;
  background-color: #72b6e0;
  margin: 10px;
  -webkit-box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
  -moz-box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
  box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
}
.state_display {
  position: absolute;
  right: 10px;
  bottom: 10px;
}
</style>