<template>
  <div class="container">
    <h1 class="welcome-text">Добро пожаловать в Кухню, {{ userName }}!</h1>
    <button class="welcome-button" @click="showUserId">Нажми меня</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Данные пользователя
const userName = ref('Гость');
const userId = ref(null);

onMounted(() => {
  // Добавляем задержку перед инициализацией Telegram API
  setTimeout(() => {
    try {
      console.log('Проверка объекта Telegram через 1 секунду...');
      console.log('Текущий URL:', window.location.href);

      if (window.Telegram) {
        console.log('Объект Telegram:', window.Telegram);

        if (window.Telegram.WebApp) {
          const tg = window.Telegram.WebApp;
          console.log('Telegram WebApp API доступен:', tg);

          // Проверка initDataUnsafe
          if (tg.initDataUnsafe?.user) {
            console.log('Данные пользователя:', tg.initDataUnsafe.user);
            userName.value = tg.initDataUnsafe.user.first_name || 'Гость';
            userId.value = tg.initDataUnsafe.user.id;
          } else {
            console.warn('Данные пользователя недоступны.');
          }
        } else {
          console.error('Telegram WebApp API отсутствует.');
        }
      } else {
        console.error('Объект Telegram недоступен.');
      }
    } catch (error) {
      console.error('Ошибка при инициализации Telegram API:', error);
    }
  }, 1000); // Задержка 1 секунда
});

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
