<template>
 <div id="app" class="small-container">
   <br>
   <img src="./assets/logo.png" width="100px" height="100px">
   <br>
   <h1 class="textt">ToDoList</h1>
   <br>
  <br>
  <employee-form @add:employee="addEmployee" />
  <employee-table :employees="employees" @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"
    />
  </div>
</template>

<script>
import EmployeeTable from './components/EmployeeTable.vue'
import EmployeeForm from './components/EmployeeForm.vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data () {
    return {
      employees: [
        {
          id: 1,
          name: 'one dev',
          email: 'test1@gmail.com',
          completed: false
        },
        {
          id: 2,
          name: 'Two dev',
          email: 'test2@gmail.com',
          completed: false
        },
        {
          id: 3,
          name: 'Three dev',
          email: 'test3@gmail.com',
          completed: false
        }
      ]
    }
  },
  methods: {
    addEmployee (employee) {
      const lastId =
        this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0
      const id = lastId + 1
      const newEmployee = {...employee, id}
      this.employees = [...this.employees, newEmployee]
      console.log(this.employees)
    },
    deleteEmployee (id) {
      this.employees = this.employees.filter(employee => employee.id !== id)
    },
    editEmployee (id, updatedEmployee) {
      this.employees = this.employees.map(employee => employee.id === id ? updatedEmployee : employee)
    },
    completed (employee) {
      employee.completed = !employee.completed
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: auto;
  color: #2c3e50;
}
.small-container {
  max-width:  100%;
}
</style>
