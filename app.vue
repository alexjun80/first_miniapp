<template>
  <div class="container">
    <h1 class="welcome-text">Добро пожаловать в Кухню, {{ userName }}!</h1>
    <button class="welcome-button" @click="showWindowProperties">Показать свойства window</button>
    <pre v-if="windowProperties">{{ windowProperties }}</pre>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Переменные для данных
const userName = ref('Гость');
const windowProperties = ref(null);

// Функция для вывода всех свойств объекта window
const showWindowProperties = () => {
  try {
    // Сериализуем объект window и сохраняем его свойства в формате JSON
    const properties = Object.keys(window).reduce((acc, key) => {
      acc[key] = window[key];
      return acc;
    }, {});
    windowProperties.value = JSON.stringify(properties, null, 2);

    // Выводим свойства в консоль
    console.log('Свойства объекта window:', properties);

    // Также можно вывести всплывающее окно
    alert('Свойства объекта window записаны в консоль.');
  } catch (error) {
    console.error('Ошибка при получении свойств window:', error);
    alert('Ошибка при получении свойств window.');
  }
};
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

.welcome-button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #d32f2f;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.welcome-button:hover {
  background-color: #b71c1c;
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
