<template>
  <div id="app">
    <div class="container">
      <AddEmployeeForm @add-employee="addEmployee" />
      <EmployeeList :employees="employees" @remove-employee="removeEmployee" />
    </div>
  </div>
</template>

<script>
import AddEmployeeForm from "./components/AddEmployeeForm.vue";
import EmployeeList from "./components/EmployeeList.vue";

export default {
  components: {
    AddEmployeeForm,
    EmployeeList,
  },
  data() {
    return {
      employees: [], 
    };
  },
  methods: {
    addEmployee(employee) {
      if (employee.name.trim() === "") {
        alert("Ф.И.О. не может быть пустым!");
        return;
      }
      this.employees.push(employee);
    },
    removeEmployee(index) {
      // Удаление сотрудника по индексу
      this.employees.splice(index, 1);
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  max-width: 1200px;
  margin: 20px auto;
  padding: 20px;
  background: #f7f7f7;
  border-radius: 10px;
}

.container {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}
</style>
