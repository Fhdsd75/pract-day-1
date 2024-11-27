<template>
    <div class="table-container">
      <h2>Учет товара</h2>
      <table class="employee-table">
        <thead>
          <tr>
            <th>#</th>
            <th>Название товара</th>
            <th>Дата приема товара</th>
            <th>Количество</th>
            <th>Цена за единицу товара</th>
            <th>Действия</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(employee, index) in employees"
            :key="index"
            class="table-row"
          >
            <td>{{ index + 1 }}</td>
            <td>{{ employee.name }}</td>
            <td>{{ employee.date }}</td>
            <td>{{ employee.daysWorked }}</td>
            <td>{{ employee.salary.toFixed(2) }}</td>

            <td>
              <button class="btn-danger" @click="removeEmployee(index)">
                Удалить
              </button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <div class="totals">
        <p><strong>Общая сумма(в Тенге):</strong> {{ totalSalary }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['employees'],
    methods: {
      calculateTaxedSalary(salary) {
        return (salary * 0.85).toFixed(2);
      },
      removeEmployee(index) {
        this.$emit('remove-employee', index);
      },
    },
    computed: {
      totalSalary() {
        return this.employees.reduce((total, emp) => total + emp.salary, 0).toFixed(2);
      },
      totalSalaryAfterTax() {
        return this.employees.reduce((total, emp) => total + emp.salary * 0.85, 0).toFixed(2);
      },
    },
  };
  </script>
  
  <style scoped>
  .table-container {
    padding: 20px;
    background: #c100f144;
    border-radius: 10px;
    box-shadow: 0 10px 10px rgba(249, 0, 166, 0.5);
  }
  
  h2 {
    margin-bottom: 20px;
    text-align: center;
    color: #333;
  }
  
  .employee-table {
    width: 100%;
    border-collapse: collapse;
    background: #c100f144;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 10px 10px rgba(127, 8, 255, 0.377);
  }
  
  .employee-table th,
  .employee-table td {
    text-align: left;
    padding: 12px;
    border-bottom: 1px solid #ddd;
    color: #000;
  }
  
  .employee-table th {
    background: #b900f7;
    color: #ffffff;
    font-weight: bold;
  }
  
  .employee-table tr:nth-child(even) {
    background: #f4f4f4;
  }
  
  .employee-table tr:hover {
    background: #f1f9ff;
  }
  
  .btn-danger {
    background-color: #e74c3c;
    color: white;
    border: none;
    padding: 8px 12px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .btn-danger:hover {
    background-color: #c0392b;
  }
  
  .totals {
    margin-top: 20px;
    font-size: 1.1rem;
    color: #333;
  }
  
  .totals p {
    margin: 5px 0;
  }
  </style>
  