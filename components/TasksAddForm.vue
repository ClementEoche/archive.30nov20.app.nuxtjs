<template>
  <div class="content-inputs">
    <vs-input class="mb-4" v-model="titleInput" label="Title" placeholder="My task" style="margin-bottom: 20px"/>
    <vs-input class="mb-4" v-model="descriptionInput" label="Description" placeholder="This is a task" style="margin-bottom: 20px"/>
    <vs-button flat dark @click="addTask">
      Add
    </vs-button>
  </div>
</template>

<script>
export default {
  name: "TasksAddForm",
  data: () => ({
    titleInput: '',
    descriptionInput: '',
    doneInput: false
  }),
  methods: {
    async addTask(){
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
      await this.$axios.$post('/api/tasks',
        {
          "title" : this.titleInput,
          "description" : this.descriptionInput,
          "done" : this.doneInput
        }, {headers}).then(function (response) {
          location.reload()
        }
      )
    }
  }
}
</script>

<style scoped>

</style>
