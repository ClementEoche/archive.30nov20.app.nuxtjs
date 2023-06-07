<template>
  <div class="grid" style="margin-top: 100px">
    <vs-row>
      <navbar page="tasks"></navbar>
    </vs-row>
    <vs-row justify="space-around">
      <vs-col w="2">
        <h5 style="margin-bottom: 20px">Add a task</h5>
        <TasksAddForm></TasksAddForm>
        <div id="updateContainer" class="hidden">
          <h5 style="margin-bottom: 20px; margin-top: 40px">Update a task</h5>
          <TasksUpdateForm v-on:cancelButton="handleCancel" v-bind:task="selectedTask"></TasksUpdateForm>
        </div>
      </vs-col>
      <vs-col w="5">
        <h5 style="margin-bottom: 20px">My tasks</h5>
        <TasksList v-on:updateButton="handleUpdate($event)"></TasksList>
      </vs-col>
    </vs-row>
  </div>
</template>

<script>
import Navbar from "@/components/navbar";
import TasksList from "@/components/TasksList";
import TasksAddForm from "@/components/TasksAddForm";
import TasksUpdateForm from "@/components/TasksUpdateForm";

export default {
  name: "tasks",
  data: () => ({
    selectedTask: []
  }),
  methods: {
    handleUpdate(task){
      document.getElementById("updateContainer").classList.remove("hidden")
      this.selectedTask = task
    },
    handleCancel(){
      document.getElementById("updateContainer").classList.add("hidden")
    }
  },
  created() {
    if (process.browser) {
      if (localStorage.getItem('jwt') == null) {
        this.$router.push('/')
      }
    }
  },
  components: {TasksUpdateForm, TasksAddForm, TasksList, Navbar}
}
</script>

<style scoped>

</style>
