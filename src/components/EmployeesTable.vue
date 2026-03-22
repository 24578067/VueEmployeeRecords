<script>
import MyButton from './UI/MyButton.vue'

export default {
  components: {
    MyButton,
  },
  props: {
    employees: {
      type: Array,
    },
  },
  emits: ['edit-empl', 'delete-empl'],
}
</script>

<template>
  <div class="table-wrapper">
    <table class="table">
      <thead class="table__head">
        <tr class="table__row table__row--header">
          <th class="table__cell table__cell--header">ID</th>
          <th class="table__cell table__cell--header">ФИО</th>
          <th class="table__cell table__cell--header">Зарплата</th>
          <th class="table__cell table__cell--header">Возраст</th>
          <th class="table__cell table__cell--header"></th>
        </tr>
      </thead>
      <tbody class="table__body">
        <tr
          class="table__row"
          v-for="employee in employees"
          :key="employee.id"
          @dblclick="$emit('edit-empl', employee)"
        >
          <td class="table__cell">{{ employee.id }}</td>
          <td class="table__cell">{{ employee.employee_name }}</td>
          <td class="table__cell">{{ employee.employee_salary }}</td>
          <td class="table__cell">{{ employee.employee_age }}</td>
          <td class="table__cell">
            <MyButton class="btn-table btn--delete" @click="$emit('delete-empl', employee)"
              >Удалить</MyButton
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
/* ===== Таблица ===== */
.table-wrapper {
  background: #ffffff;
  border-radius: 6px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  overflow-x: auto;
  border: 1px solid #ecf0f1;
  margin-bottom: 50px;
}

.table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.95rem;
}

/* Шапка таблицы - синяя (нейтральная, информационная) */
.table__head {
  background: #3498db;
  color: #ffffff;
}

.table__row--header .table__cell--header {
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 0.5px;
  padding: 16px 20px;
}

.table__row {
  transition: all 0.2s ease;
}

/* Hover на строке — светло-синий оттенок */
.table__row:not(.table__row--header):hover {
  background-color: #ebf5fb;
  cursor: pointer;
  border-left: 3px solid #3498db;
  padding-left: 17px;
}

.table__cell {
  padding: 16px 20px;
  text-align: left;
  border-bottom: 1px solid #ecf0f1;
  color: #2c3e50;
}

.table__cell:last-child {
  text-align: center;
}

.table__row--header .table__cell--header {
  padding: 16px 20px;
  font-weight: 600;
  color: #ffffff;
}

.table__body .table__row:last-child .table__cell {
  border-bottom: none;
}

/* Акцент на ID колонке - синий */
.table__cell:first-child {
  font-weight: 600;
  color: #3498db;
}

/* Чётные строки — лёгкий фон */
.table__body .table__row:nth-child(even) {
  background-color: #f8f9fa;
}

.table__body .table__row:nth-child(even):hover {
  background-color: #ebf5fb;
}
</style>
