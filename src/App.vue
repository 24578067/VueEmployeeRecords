<script>
import axios from 'axios'
import AppHeader from './components/AppHeader.vue'
import EmployeesTable from './components/EmployeesTable.vue'
import MyModal from './components/UI/MyModal.vue'

export default {
  components: {
    AppHeader,
    EmployeesTable,
    MyModal,
  },
  data() {
    return {
      employees: [],
      modalVisible: false,
      form: {
        employee_name: '',
        employee_salary: '',
        employee_age: '',
      },
      editMode: false,
      editingId: null,
    }
  },
  methods: {
    async fetchEmployee() {
      try {
        const response = await axios.get('https://dummy.restapiexample.com/api/v1/employees')
        this.employees = response.data.data
      } catch (e) {
        alert(`Не удалось загрузить сотрудников: ${e.message}`)
      }
    },

    openModal() {
      this.form = {
        employee_name: '',
        employee_salary: '',
        employee_age: '',
      }
      this.editMode = false
      this.editingId = null
      this.modalVisible = true
    },

    closeModal() {
      this.modalVisible = false
    },

    handleModalSubmit(formData) {
      if (this.editMode) {
        const index = this.employees.findIndex((emp) => emp.id === this.editingId)
        if (index !== -1) {
          this.employees[index] = {
            id: this.editingId,
            ...formData,
          }
        }
      } else {
        const newId =
          this.employees.length > 0 ? Math.max(...this.employees.map((e) => e.id)) + 1 : 1
        this.employees.push({
          id: newId,
          ...formData,
        })
      }
      this.closeModal()
    },

    deleteEmployee(employee) {
      this.employees = this.employees.filter((emp) => emp.id !== employee.id)
    },

    editEmployee(employee) {
      this.editMode = true
      this.editingId = employee.id
      this.form = { ...employee }
      this.modalVisible = true
    },
  },
  mounted() {
    this.fetchEmployee()
  },
}
</script>

<template>
  <div class="app">
    <div class="container">
      <MyModal
        :model-value="modalVisible"
        :form="form"
        :edit-mode="editMode"
        @update:model-value="modalVisible = $event"
        @update:form="form = $event"
        @submit="handleModalSubmit"
        @close="closeModal"
      />

      <AppHeader @add-click="openModal" />
      <EmployeesTable
        :employees="employees"
        @delete-empl="deleteEmployee"
        @edit-empl="editEmployee"
      />
    </div>
  </div>
</template>

<style></style>
