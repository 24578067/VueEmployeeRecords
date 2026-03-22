<script>
export default {
  name: 'MyButton',
}
</script>

<template>
  <button>
    <slot></slot>
  </button>
</template>

<style scoped>
.btn {
  width: 250px;
  padding: 14px 24px;
  font-size: 15px;
  font-weight: 600;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.btn-table {
  padding: 14px 24px;
  font-size: 15px;
  font-weight: 600;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.btn:active {
  transform: translateY(0);
}

/* Кнопка ДОБАВИТЬ - зелёная */
.btn--add {
  background: #27ae60;
}

.btn--add:hover {
  background: #219a52;
}

/* Кнопка УДАЛИТЬ - красная */
.btn--delete {
  background: #e74c3c;
}

.btn--delete:hover {
  background: #c0392b;
}
</style>
