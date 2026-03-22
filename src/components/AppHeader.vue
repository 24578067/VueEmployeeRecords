<script>
import MyButton from './UI/MyButton.vue'

export default {
  components: {
    MyButton,
  },
  emits: ['add-click'],
}
</script>

<template>
  <header class="header">
    <h1>Учет сотрудников</h1>
    <div class="btns">
      <MyButton class="btn btn--add" @click="$emit('add-click')">Добавить сотрудника</MyButton>
    </div>
  </header>
</template>

<style scoped>
/* ===== Header ===== */
.header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
  margin: 50px;
}

.header h1 {
  color: #2c3e50;
  font-size: 2rem;
  font-weight: 700;
  margin: 0;
}

/* ===== Кнопки ===== */
.btns {
  display: flex;
  gap: 50px;
}
</style>
