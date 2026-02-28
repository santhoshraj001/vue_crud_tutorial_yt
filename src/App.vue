<template>
  <div id="small-container">
  <h1>Welcome to this form {{ employeename }}</h1>
  <Employee-Forms @update-name="receiveName" @employee-updated="receiveEmployee" @employee-details="receiveDetails"/> <!-- this @employee-updated  this is custom emit event name from employee_form and receiveEmployee is method name -->
                                                
  <Employee-Table :employees="employees"/>   <!-- this :employees="employees" this is attribute call in data function reactive datas (key:peoperty)  we can use in child component like a props-->
                                                <!-- : means v-bind
                                                      Parent passes its employees data
                                                     Child component receives it as a prop and displays it in a table -->
  </div>
  
</template>

<script>
import EmployeeTable from './components/employee_table.vue'
import EmployeeForms from './components/employee_forms.vue'


export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForms  // importing employee form component to app.vue and using in template tag
   
  },
  data() {
    return {
      employeename: '',   // its for live typing showing on head tag
      employees: [
        {id: 1, name: 'John Doe', email: 'john@example.com', 
        office: 'Covai', age: 25, salary: 55000 },   //this is reactive data
        {id: 2, name: 'Jane Smith', email: 'jane@example.com', 
        office: 'Chennai', age: 30, salary: 60000 }, // this name is one property and all fields name is call like a property
      ],
    }
  },

  methods: {
     receiveEmployee(data) {
    console.log("From Child:", data)
  },
  receiveDetails(employee) {
    const newEmployee = { ...employee, id: this.employees.length + 1 }  // this is new object and this is add id property in form data and this is one way data flow from child to parent component
    this.employees = [...this.employees, newEmployee]  //(...this.employees means old employees array) this is push form data to employees array and this is one way data flow from child to parent component
   //  this.employees.push(employee)   //this is another same method to add value in employees array
  },

  receiveName(name) {
    this.employeename = name
  }

}
}

</script>


<style>
#small-container{
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}


</style>
