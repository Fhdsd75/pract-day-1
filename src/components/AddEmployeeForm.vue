<template>
    <div class="form-container">
      <h2>Добавить учет товара</h2>
      <form @submit.prevent="handleAddEmployee">
        <div class="form-group">
          <label for="name">Название Товара</label>
          <input
            type="text"
            id="name"
            v-model="name"
            placeholder="Введите Название Товара"
            required
          />
        </div>
        <div class="form-group">
          <label for="date">Дата приема товара</label>
          <input
            type="date"
            id="date"
            v-model="date"
            required
          />
        </div>
        <div class="form-group">
          <label for="daysWorked">Количество товара</label>
          <input
            type="number"
            id="daysWorked"
            v-model="daysWorked"
            placeholder="Количество товара"
            min="1"
            required
          />
        </div>
        <div class="form-group">
          <label for="salary">Цена за товар</label>
          <input
            type="number"
            id="salary"
            v-model="salary"
            placeholder="Цена товара"
            min="1"
            required
          />
        </div>
        <button type="submit" class="btn-primary">Добавить</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: ["onAddEmployee"],
    data() {
      return {
        name: "", 
        date: "", 
        daysWorked: "", 
        salary: "", 
      };
    },
    methods: {
      handleAddEmployee() {
        if (
          this.name.trim() === "" || // Проверка, чтобы Ф.И.О. не было пустым
          this.date === "" || // Проверка дату
          this.daysWorked <= 0 || // Проверка, чтобы дни были больше 0
          this.salary <= 0 // Проверка чтобы зарплата была больше 0
        ) {
          alert("Все поля обязательны для заполнения!");
          return;
        }
        this.$emit("add-employee", {
          name: this.name,
          date: this.date,
          daysWorked: Number(this.daysWorked),
          salary: Number(this.salary),
        });
        this.name = "";
        this.date = "";
        this.daysWorked = "";
        this.salary = "";
      },
    },
  };
  </script>
  
  <style scoped>
  .form-container {
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
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .form-group label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #000000;
  }
  
  .form-group input {
    width: 100%;
    padding: 10px;
    border: 1px solid #7d197373;
    border-radius: 5px;
    font-size: 1rem;
    color: #000000;
  }
  
  .form-group input::placeholder {
    color: #aaa;
  }
  
  .btn-primary {
    display: block;
    width: 100%;
    background-color: #e600ff;
    color: rgb(255, 255, 255);
    padding: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
    box-shadow: 0 10px 10px rgba(249, 0, 166, 0.5);
  }
  
  .btn-primary:hover {
    background-color: #ff0080;
  }
  </style>
  