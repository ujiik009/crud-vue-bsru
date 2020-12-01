<template>
  <div class="center">
    <KanBanBoard
      :data="data"
      :move_task="move_task"
      :create_task_handle="create_task_handle"
    />
  </div>
</template>

<script>
import KanBanBoard from "./components/KanBanBoard";
import moment from "moment";
export default {
  components: {
    KanBanBoard,
  },
  methods: {
    move_task(column_a, index_task_a, column_b, index_task_b) {
      var item = this.data[column_a].task[index_task_a];
      // remove before
      this.data[column_a].task.splice(index_task_a, 1);
      // move to
      this.data[column_b].task.splice(index_task_b, 0, item);
    },
    create_task_handle(column_index, item) {
      item.created_at = moment().format("YYYY-MM-DD HH:mm:ss")
      this.data[column_index].task.push(item);
    },
  },
  data() {
    return {
      data: [
        {
          state: "todo",
          color: "#CC5C5A",
          task: [],
        },
        {
          state: "doing",
          color: "#EB7145",
          task: [],
        },
        {
          state: "done",
          color: "#EACA78",
          task: [],
        },
      ],
    };
  },
};
</script>

<style>
.modal-backdrop {
  background-color: rgba(119, 119, 119, 0.837) !important;
}
</style>