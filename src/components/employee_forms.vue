<template>
 
  <div class="one">
     <form v-on:submit.prevent="handlesubmit">   <!-- .prevent stop the page reload -->
    <label for="name">Name: </label>
    <input type="text" id="name" v-model="employee.name">
    <p style="color: red">{{ errors.name }}</p>
    <label for="email">Email:</label>
    <input type="email" id="email" v-model="employee.email">
    <p style="color: red">{{ errors.email }}</p>
    <label for="office">Office:</label>
    <input type="text" id="office" v-model="employee.office">
    <p style="color: red">{{ errors.office }}</p>
    <label for="age">Age:</label>
    <input type="number" id="age" v-model="employee.age">
    <p style="color: red">{{ errors.age }}</p>
    <label for="salary">Salary:</label>
    <input type="number" id="salary" v-model="employee.salary">
    <p style="color: red">{{ errors.salary }}</p>
    <button type="submit">Add Employee</button>
    </form>
  </div>
</template>
<script>
export default {
  name: 'Employee-Forms',
  data() {
    return {
        errors: {
         name: null,
         email: null,
         office: null,
         age: null,
         salary: null,    

        },
      // form data can be added here
      employee: {
        id: null,
        name: '',   // this is name property for receiving form data and this is reactive data , call in input field like(v-model="employee.name") and this is one property for receiving form data and all fields name is call like a property
        email: '',
        office: '',
        age: null,
        salary: null,
      },
    }
  },
  watch: {
    employee: {
      handler(newValue) {
        // send updated employee to parent
      this.$emit('employee-updated', newValue)   //employee-updated is custom event name and newValue is form data and this is send to parent component like app.vue and this is one way data flow from child to parent component
      },
        deep: true
    },
    'employee.name'(newValue) {
    this.$emit('update-name', newValue)
  },
  },

  methods:{
    resetForm() {
    this.employee = {
      id: null,
      name: '',
      email: '',
      office: '',
      age: null,
      salary: null
    }

    this.errors = {}
  },

    validateForm() {

    this.errors = {}

    if (!this.employee.name) {
      this.errors.name = "Name is required"
    }

    if (!this.employee.email) {
      this.errors.email = "Email is required"
    }

    if (!this.employee.office) {
      this.errors.office = "Office is required"
    }

    if (!this.employee.age) {
      this.errors.age = "Age is required"
    }

    if (!this.employee.salary) {
      this.errors.salary = "Salary is required"
    }

  },
   handlesubmit(){
      this.validateForm()

  if (!this.invalidform) {
    return
  }
        // alert('add details first')
        this.$emit('employee-details', this.employee)  // this.employee is data object and value property, this is send form data to parent component like app.vue and this is one way data flow from child to parent component
       this.resetForm()
    },
    
  },
computed: {
  invalidform() {
    return Object.keys(this.errors).length === 0
  }
}
}
</script>

<style scoped>
.one {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 300px;
  margin-left: auto;
  margin-right: auto;
}
#employee-forms {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 300px;
  margin-left: auto;
    margin-right: auto;
  
}   
form {
  display: flex;
  flex-direction: column;
}
label {
  margin-top: 10px;
}
input {
  padding: 5px;
  margin-top: 5px;
}
button {
  margin-top: 20px;
  padding: 10px;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
</style>