<template>
  <div id="kanban-body">
    <div
      class="column"
      :style="{ backgroundColor: column.color }"
      v-for="(column, column_index) in data"
      :key="column_index"
    >
      <!-- header column -->
      <div class="column-header" style="display: flex">
        {{ column.state }}
      </div>
      <!-- header column -->
      <div
        class="column-body"
        @drop="drop"
        @dragover.prevent
        @dragenter.prevent
      >
        <div
          v-for="(item, item_index) in column.task"
          :key="item_index"
          
        >
          <Task
            :item="item"
            :column_index="column_index"
            :item_index="item_index"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Task from "./Task";
export default {
  props: {
    data: Array,
  },
  components: { Task },
  methods: {
    show() {
      alert(555);
    },
    dragstart() {
      console.log("dragstart");
    },
    drop() {
      alert("drop");
    },
  },
};
</script>

<style scoped>
#kanban-body {
  width: 100%;
  background-color: bisque;
  height: 100vh;
  /* overflow: auto; */
}
.column {
  height: 500px;
  width: 300px;
  border-radius: 10px;
  background-color: blue;
  display: inline-block;
  margin: 25px;
  padding: 10px;
}
.column-header {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  font-size: 32px;
  font-weight: bold;
}
.column-body {
  background-color: rgba(255, 255, 255, 0.576);
  height: calc(100% - 50px);
  border-radius: 10px;
  padding: 5px;
  overflow: auto;
}
.task {
  width: auto;
  border-radius: 10px;
  height: 100px;
  background-color: #72b6e0;
  margin: 10px;
}
</style>