<template>
  <vs-table striped>
    <template #thead>
      <vs-tr>
        <vs-th>
          Title
        </vs-th>
        <vs-th>
          Description
        </vs-th>
        <vs-th>
        </vs-th>
      </vs-tr>
    </template>
    <template #tbody>
      <vs-tr :key="i" v-for="(tr, i) in tasks" :data="tr">
        <vs-td>
          {{ tr.title }}
        </vs-td>
        <vs-td>
          {{ tr.description }}
        </vs-td>
        <vs-td>
          <vs-button flat color="warn" icon @click="updateButton(tr)">
          </vs-button>
          <vs-button flat color="danger" icon @click="deleteButton(tr.id)">
          </vs-button>
        </vs-td>
      </vs-tr>
    </template>
  </vs-table>
</template>

<script>
export default {
  name: "TasksList",
  data: () => ({
    tasks: []
  }),
  methods: {
    async getTasks() {
      var jwt
      if (process.browser) {
        if (localStorage.getItem('jwt') != null) {
          jwt = localStorage.getItem('jwt')
        
      const headers ={
          'x-access-token': jwt
        }
      const tasks = await this.$axios.$get('/api/tasks', {headers})
      this.tasks = tasks
      }
      }
    },
    updateButton(task) {
      this.$emit('updateButton', task)
    },
    async deleteButton(id) {
      var jwt
      if (process.browser) {
        if (localStorage.getItem('jwt') != null) {
          jwt = localStorage.getItem('jwt')
        }
      }
      const headers ={
        'x-access-token': jwt
      }
      await this.$axios.$delete('/api/tasks/' + id, {headers}).then(function () {
        location.reload()
      })
    }
  },
  created() {
    this.getTasks()
  }
}
</script>

<style scoped>

</style>
