<template>
  <div id="kanban-body" class="center">
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

      <!-- body column -->
      <div class="column-body">
        <Task
          v-for="(task, task_index) in column.task"
          :key="task_index"
          @dragstart="dragstart(column_index, task_index)"
          :item="task"
          :column_index="column_index"
          :task_index="task_index"
        >
          <div
            @dragenter.prevent="drop_zone_enter"
            @dragover.prevent
            @dragleave.prevent="drop_zone_leave"
            @drop="drop(column_index, task_index)"
            class="drop_zone"
          >
            <!-- drop zone -->
          </div>
        </Task>
        <div
          @dragenter.prevent="drop_zone_enter"
          @dragleave.prevent="drop_zone_leave"
          @dragover.prevent
          @drop="drop(column_index, column.task.length)"
          class="drop_zone"
        >
          <!-- drop zone -->
        </div>
        <div class="create_task" @click="create_task(column_index)">
          <svg
            width="1em"
            height="1em"
            viewBox="0 0 16 16"
            class="bi bi-plus"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"
            />
          </svg>
          Create Task
        </div>
      </div>
      <!-- body column -->
    </div>
    <!-- modal settion -->
    <b-modal ref="create_task" hide-footer title="Create Your Task">
      <div class="d-block text-center">
        <b-form-textarea
          id="textarea"
          v-model="name_task"
          placeholder="Enter something..."
          rows="3"
          max-rows="6"
          @keyup.13="submit_create_task"
        ></b-form-textarea>
        {{ name_task }}
      </div>
    </b-modal>
    <!-- modal settion -->
  </div>
</template>

<script>
import Task from "./Task";
export default {
  props: {
    data: Array,
    move_task: Function,
    create_task_handle: Function,
  },
  components: { Task },
  data() {
    return {
      current_column_index: null,
      current_task_index: null,
      name_task: "",
    };
  },
  methods: {
    create_task(column_index) {
      this.$refs["create_task"].show();
      this.current_column_index = column_index;
    },
    submit_create_task() {
      this.create_task_handle(this.current_column_index, { name: this.name_task });
      this.name_task = "";
       this.$refs["create_task"].hide()
    },
    drop_zone_enter(event) {
      event.target.style.height = "100px";
      event.target.style.borderStyle = "dotted";
      event.target.style.transition = "height 0.5s";
      event.pre;
    },
    drop_zone_leave(event) {
      event.target.style.height = "10px";
      event.target.style.transition = "height 0.5s";
      event.target.style.borderStyle = "none";
    },
   
    dragstart(column_index, task_index) {
      this.current_column_index = column_index;
      this.current_task_index = task_index;
      console.log("dragstart");
    },
    drop(column_index, task_index) {
      event.target.style.height = "10px";
      event.target.style.transition = "height 0.5s";
      event.target.style.borderStyle = "none";
      this.move_task(
        this.current_column_index,
        this.current_task_index,
        column_index,
        task_index
      );
    },
  },
};
</script>

<style scoped>
.create_task {
  width: 100%;
  height: auto;
  padding: 10px;

  border-radius: 5px;
  cursor: pointer;
}
.create_task:hover {
  background-color: #cecece;
}
.drop_zone {
  height: 10px;
  /* background-color: brown; */
}
#kanban-body {
  width: 100%;
  background-color: bisque;
  height: 100vh;
  /* overflow: auto; */
}
.column {
  height: 650px;
  width: 300px;
  border-radius: 10px;
  background-color: blue;
  display: inline-block;
  margin: 25px;
  padding: 10px;
   -webkit-box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
  -moz-box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
  box-shadow: 0px 0px 5px 0px rgba(97, 97, 97, 1);
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
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 60%;
}
</style>