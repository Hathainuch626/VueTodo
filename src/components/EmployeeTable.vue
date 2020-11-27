<template>
    <div id="employee-table">
        <p v-if="employees.length < 1" class="empty-table">
          No Data
        </p>
        <table>
            <thead>
                <tr>
                    <th>...</th>
                    <th>Full name</th>
                    <th>Email</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="employee in employees" :key="employee.id">
                    <td>
                      <input type="checkbox" v-model="employee.completed" @click="completed(employee)">
                    </td>
                    <td v-if="editing == employee.id">
                      <input type="text" v-model="employee.name">
                    </td>
                    <td v-else :style="employee.completed &&  {textDecoration: 'line-through'}">
                    {{ employee.name }}</td>
                    <td v-if="editing == employee.id">
                      <input type="text" v-model="employee.email">
                    </td>
                    <td v-else :style="employee.completed &&  {textDecoration: 'line-through'}" >{{ employee.email }}</td>
                    <td v-if="editing === employee.id">
                      <b-button variant="success" @click="editEmployee(employee)">Save</b-button>
                      <b-button variant="info" class="muted-button" @click="cancelEdit(employee)">Cancel</b-button>
                    </td>
                    <td v-else>
                      <b-button variant="warning" @click="editMode(employee)">Edit</b-button>
                      <b-button variant="danger" @click="$emit('delete:employee', employee.id)">Delete</b-button>
                    </td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<script>
export default {
  name: 'employee-table',
  data () {
    return {
      editing: null
    }
  },
  methods: {
    editMode (employee) {
      this.cachedEmployee = Object.assign({}, employee)
      this.editing = employee.id
    },

    cancelEdit (employee) {
      Object.assign(employee, this.cachedEmployee)
      this.editing = null
    },

    editEmployee (employee) {
      if (employee.name === '' || employee.email === '') return
      this.$emit('edit:employee', employee.id, employee)
      this.editing = null
    },

    completed (employee) {
      employee.completed = !employee.completed
    }
  },
  props: {
    employees: Array
  }
}
</script>
<style scoped>
.empty-table {
  font-weight: bold;
  font-size: 1.3rem;
  background: rgb(231, 217, 137);
  color: #000;
  padding: .5rem 1rem;
}
table {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  margin: auto;
}

table td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even){background-color: #f2f2f2;}

table tr:hover {background-color: #ddd;}

table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #e96a16;
  color: white;
}
</style>
