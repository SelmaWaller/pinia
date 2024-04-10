<script>
import { ref } from "vue";
import { useTaskStore } from "~/src/stores/TaskStore";
import TaskDetails from "~/src/components/TaskDetails.vue";
import TaskForm from "../src/components/TaskForm.vue";
export default {
  components: { TaskForm, TaskDetails },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref("all");
    return { taskStore, filter };
  },
};
</script>

<template>
  <div>
    <header>
      <img src="/src/assets/img/pinia-logo.png" alt="logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <!--task form-->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!--filter-->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Favs</button>
    </nav>

    <!-- task list-->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} favorites</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;800&family=VT323&display=swap");

body {
  background: #f2f2f2;
  color: #444;
  margin: 0;
}
body * {
  font-family: "Poppins", sans-serif;
}

/* header */
header {
  text-align: center;
  background: #e7e7e7;
  padding-top: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 20px;
}
header img {
  max-width: 60px;
  transform: rotate(-10deg);
}
header h1 {
  margin: 0 0 0 15px;
  font-size: 2em;
  padding-top: 25px;
  color: #777;
  transform: rotate(2deg);
}

/* task list */
.task-list {
  max-width: 640px;
  margin: 20px auto;
}
.task {
  padding: 6px 20px;
  background: #fff;
  margin-top: 20px;
  border-radius: 4px;
  box-shadow: 2px 4px 6px rgba(0, 0, 0, 0.05);
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.task h3,
.task .icons {
  display: inline-block;
}
.task .icons {
  text-align: right;
}
.task i {
  font-size: 1.4em;
  margin-left: 6px;
  cursor: pointer;
  color: #bbb;
}
.task i.active {
  color: #ff005d;
}

/* filter nav */
.filter {
  width: 640px;
  margin: 10px auto;
  text-align: right;
}
.filter button {
  display: inline-block;
  margin-left: 10px;
  background: #fff;
  border: 2px solid #555;
  border-radius: 4px;
  padding: 4px 8px;
  cursor: pointer;
  font-size: 1em;
}

/* new task form */
.new-task-form {
  background: #e7e7e7;
  padding: 20px 0;
}
form {
  max-width: 400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 10px;
}

/* loading state */
.loading {
  max-width: 640px;
  border: 1px solid #ffd859;
  background: #ffe9a0;
  color: #3a3a3a;
  padding: 5px 0;
  text-align: center;
  margin: 30px auto;
}
</style>
