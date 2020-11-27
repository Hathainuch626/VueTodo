<template>
  <div id="employee-form" class="form">
    <form @submit.prevent="handleSubmit">
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <label>Name</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="employee.name"
      />
      <br />
      <label>Email</label>
      <input
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="employee.email"
        type="text"
      />
      <br />
      <p v-if="error && submitting" class="error-message">
        Please fill out all required fields
      </p>
      <p v-if="success && submitting" class="success-message">
        Employee successfully added
      </p>
      <button>Add Data</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'employee-form',
  data () {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: '',
        email: ''
      }
    }
  },
  methods: {
    handleSubmit () {
      this.submitting = true
      // this.clearStatus()
      if (this.invalidName || this.invalidEmail) {
        this.error = true
        return
      }
      this.$emit('add:employee', this.employee)
      this.$refs.first.focus()

      this.employee = {
        name: '',
        email: ''
      }
      this.error = false
      this.success = true
      this.submitting = false
    }
  },
  computed: {
    invalidName () {
      return this.employee.name === ''
    },
    invalidEmail () {
      return this.employee.email === ''
    }
  }
  // clearStatus () {
  // this.success = false
  // this.error = false
  // }
}

</script>
<style >
form {
  margin-bottom: 2rem;
}
input {
  padding: 10px 15px;
  margin: 8px 0;
  box-sizing: border-box;
  margin-bottom: 2rem;
  background: #ffffff;
}
input:focus {
  padding: 10px 15px;
  margin: 8px 0;
  box-sizing: border-box;
  margin-bottom: 2rem;
  background: #7e7d7d;
}
[class*="-message"] {
  font-weight: bold;
}
.error-message {
  color: #d33c40;
}
.success-message {
  color: #32a95d;
}
.form {
  margin-top: -200px;
}
button {
  background: #1da04d;
  border: 1px solid #009435;
  padding: .8em;
  color: #ffff;
}
</style>
