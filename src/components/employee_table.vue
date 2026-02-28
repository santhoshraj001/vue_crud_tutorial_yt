<template>
    <div id="employee-table">
        <h1>Employee Table</h1>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>email</th>
                    <th>Office</th>
                    <th>Age</th>
                   
                    <th>Salary</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="employee in employees" :key="employee.id">
                    <td>{{ employee.name }}</td>
                    <td>{{ employee.email }}</td>
                    <td>{{ employee.office }}</td>
                    <td>{{ employee.age }}</td>
                    <td>{{ employee.salary }}</td>
                    
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: 'Employee-Table' ,  // this is component name use in app.vue inside template tag
    props: {
        employees: Array, // this data type is array and this is to receive data from parent component (app.vue)
    }  
}

</script>
<style scoped>
#employee-table {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
</style>
   