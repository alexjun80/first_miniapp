<template>
  <div class="container">
    <h1 class="welcome-text">Добро пожаловать в Кухню, {{ userName }}!</h1>
    <pre v-if="windowProperties">{{ windowProperties }}</pre>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Переменные для данных
const userName = ref('Гость');
const windowProperties = ref(null);

// Отображаем свойства объекта window сразу после загрузки
onMounted(() => {
  try {
    // Собираем ключи объекта window
    const properties = Object.keys(window).join(', ');
    windowProperties.value = properties;

    // Логируем свойства в консоль
    console.log('initData:', window.Telegram?.WebApp?.initData);
    console.log('Свойства объекта window:', properties);

    // Дополнительная диагностика для Telegram WebApp API
    if (window.Telegram) {
      console.log('Объект Telegram доступен:', window.Telegram);
    } else {
      console.error('Объект Telegram недоступен.');
    }
  } catch (error) {
    console.error('Ошибка при получении свойств window:', error);
    windowProperties.value = 'Ошибка при получении свойств window.';
  }
});
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #fff9c4;
}

.welcome-text {
  color: #d32f2f;
  font-size: 2rem;
  text-align: center;
}

pre {
  margin-top: 20px;
  padding: 10px;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  max-height: 300px;
  overflow: auto;
  width: 90%;
  white-space: pre-wrap;
  word-wrap: break-word;
}
</style>
