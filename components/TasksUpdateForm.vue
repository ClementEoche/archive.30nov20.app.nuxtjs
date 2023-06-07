<template>
  <div class="content-inputs">
    <vs-input v-model="task.title" label="Title" style="margin-bottom: 20px"/>
    <vs-input v-model="task.description" label="Description" style="margin-bottom: 20px"/>
    <vs-row>
      <vs-button flat dark @click="updateTask">
        Update
      </vs-button>
      <vs-button flat dark @click="cancelButton">
        Cancel
      </vs-button>
    </vs-row>
  </div>
</template>

<script>
export default {
  name: "TasksUpdateForm",
  props: ["task"],
  methods: {
    async updateTask() {
      var self = this
      var jwt
      if (process.browser) {
        if (localStorage.getItem('jwt') != null) {
          jwt = localStorage.getItem('jwt')
        }
      }
      const headers ={
        'x-access-token': jwt
      }
      await this.$axios.$put('/api/tasks/' + this.task.id,
        {
          "title": this.task.title,
          "description": this.task.description,
          "done": this.task.done
        }, {headers}).then(function (response) {
          location.reload()
        }
      )
    },
    cancelButton() {
      this.$emit('cancelButton')
    },
  }
}
</script>

<style scoped>

</style>
