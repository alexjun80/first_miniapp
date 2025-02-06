<template>
  <div class="container">
    <h1 class="welcome-text">Добро пожаловать в Кухню, {{ userName }}!</h1>
    <button class="welcome-button" @click="showUserId">Нажми меня</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Переменные для данных пользователя
const userName = ref('Гость');
const userId = ref(null);

onMounted(() => {
  try {
    // Проверяем доступность Telegram WebApp API
    if (window.Telegram && window.Telegram.WebApp) {
      const tg = window.Telegram.WebApp;

      // Инициализируем WebApp
      tg.ready();

      // Получаем информацию о пользователе
      const user = tg.initDataUnsafe?.user;
      if (user) {
        userName.value = user.first_name || 'Гость';
        userId.value = user.id;
        console.log('Информация о пользователе:', user);
      } else {
        console.warn('Информация о пользователе недоступна.');
      }

      // Логируем объект WebApp для проверки
      console.log('WebApp API доступен:', tg);
    } else {
      console.error('Telegram WebApp API недоступен.');
    }
  } catch (error) {
    console.error('Ошибка при инициализации Telegram API:', error);
  }
});

// Функция для отображения ID пользователя
const showUserId = () => {
  if (userId.value) {
    alert(`Ваш ID: ${userId.value}`);
  } else {
    alert('Telegram WebApp API недоступен.');
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
</style>
