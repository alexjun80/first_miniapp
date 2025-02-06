<template>
  <div class="container">
    <h1 class="welcome-text">Добро пожаловать в Кухню, {{ userName }}!</h1>
    <button class="welcome-button" @click="showUserId">Нажми меня</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Данные пользователя
const userName = ref('Гость'); // Переменная для имени пользователя
const userId = ref(null); // Переменная для ID пользователя

/*
onMounted(() => {
  setTimeout(() => {
    try {
      console.log('Доступный объект Telegram:', window.Telegram);

      if (window.Telegram) {
        if (window.Telegram.WebApp) {
          const tg = window.Telegram.WebApp;
          console.log('Инициализация WebApp API успешна:', tg);

          // Проверка наличия данных пользователя
          if (tg.initDataUnsafe?.user) {
            console.log('Данные пользователя:', tg.initDataUnsafe.user);
            userName.value = tg.initDataUnsafe.user.first_name || 'Гость';
            userId.value = tg.initDataUnsafe.user.id;
          } else {
            console.warn('Данные пользователя недоступны.');
          }
        } else {
          console.error('WebApp API отсутствует.');
        }
      } else {
        console.error('Объект Telegram недоступен.');
      }
    } catch (error) {
      console.error('Ошибка при инициализации Telegram API:', error);
    }
  }, 300); // Задержка в 300 мс для гарантии получения объекта
});
*/

onMounted(() => {
  setTimeout(() => {
    console.log('Объект window.Telegram:', window.Telegram);
    console.log('Домен текущего приложения:', window.location.hostname);
  }, 300);
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
