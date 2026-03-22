<script>
export default {
  name: 'MyModal',
  props: {
    modelValue: {
      type: Boolean,
      required: true,
    },
    form: {
      type: Object,
      required: true,
    },
    editMode: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['update:modelValue', 'update:form', 'submit', 'close'],
}
</script>

<template>
  <div class="modal" v-show="modelValue" @click.self="$emit('close')">
    <div class="modal__content">
      <h3 class="modal__title">
        {{ editMode ? 'Редактировать сотрудника' : 'Добавить сотрудника' }}
      </h3>

      <form @submit.prevent="$emit('submit', { ...form })" class="modal__form">
        <input
          type="text"
          required
          placeholder="Введите ФИО"
          :value="form.employee_name"
          @input="$emit('update:form', { ...form, employee_name: $event.target.value })"
        />
        <input
          type="number"
          required
          placeholder="Введите зарплату"
          :value="form.employee_salary"
          @input="$emit('update:form', { ...form, employee_salary: $event.target.value })"
        />
        <input
          type="number"
          required
          placeholder="Введите возраст"
          :value="form.employee_age"
          @input="$emit('update:form', { ...form, employee_age: $event.target.value })"
        />
        <button type="submit">
          {{ editMode ? 'Сохранить' : 'Добавить' }}
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
/* ===== Модальное окно ===== */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6); /* Чуть темнее для контраста */
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 20px;
  animation: fadeIn 0.2s ease;
  cursor: pointer;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.modal__content {
  background: #ffffff;
  border-radius: 8px; /* В стиле кнопок и таблицы */
  padding: 32px;
  width: 100%;
  max-width: 420px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  gap: 20px;
  animation: slideIn 0.3s ease;
  cursor: default;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.modal__form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

/* Заголовок модалки (добавь <h3> в HTML) */
.modal__title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #2c3e50;
  margin: 0 0 8px 0;
  text-align: center;
}

/* ===== Поля формы ===== */
.modal__content input {
  width: 100%;
  padding: 14px 16px;
  font-size: 1rem;
  border: 2px solid #ecf0f1;
  border-radius: 6px;
  transition: all 0.2s ease;
  box-sizing: border-box; /* Чтобы padding не ломал ширину */
}

.modal__content input::placeholder {
  color: #95a5a6;
  font-weight: 400;
}

.modal__content input:focus {
  outline: none;
  border-color: #3498db; /* Синий акцент при фокусе */
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
}

.modal__content input:hover {
  border-color: #bdc3c7;
}

/* ===== Кнопка в модалке ===== */
.modal__content button {
  width: 100%;
  padding: 14px 24px;
  font-size: 1rem;
  font-weight: 600;
  color: #ffffff;
  background: #27ae60; /* Зелёный — как кнопка «Добавить» */
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 2px 8px rgba(39, 174, 96, 0.3);
  margin-top: 8px;
}

.modal__content button:hover {
  background: #219a52;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(39, 174, 96, 0.4);
}

.modal__content button:active {
  transform: translateY(0);
}
</style>
