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
  console.log('Текущий URL:', window.location.href);
  console.log('Объект Telegram:', window.Telegram);

  if (window.Telegram && window.Telegram.WebApp) {
    const tg = window.Telegram.WebApp;
    tg.ready();
    console.log('Telegram WebApp API доступен:', tg);
  } else {
    console.error('Telegram WebApp API недоступен.');
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
