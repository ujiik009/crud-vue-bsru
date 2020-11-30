<template>
  <KanBanBoard :data="data" />
</template>

<script>
import KanBanBoard from "./components/KanBanBoard";
export default {
  components: {
    KanBanBoard,
  },
  data() {
    return {
      data: [
        {
          state: "todo",
          color: "#CC5C5A",
          task: [
               {
              name: "work 1",
            },
               {
              name: "work 2",
            },
             {
              name: "work 3",
            },
               {
              name: "work 4",
            },
             {
              name: "work 5",
            },
               {
              name: "work 6",
            },
             {
              name: "work 7",
            },
               {
              name: "work 7",
            },
          ],
        },
        {
          state: "doing",
          color: "#EB7145",
          task: [
           
              {
              name: "work 3",
            },
          ],
        },
        {
          state: "done",
          color: "#EACA78",
          task: [
         
          ],
        },
      ],
    };
  },
};
</script>

<style>
</style>