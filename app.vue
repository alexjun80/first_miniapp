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

// Подключение Telegram WebApp API
onMounted(() => {
  const tg = window.Telegram.WebApp;

  // Установка данных пользователя
  if (tg?.initDataUnsafe?.user) {
    userName.value = tg.initDataUnsafe.user.first_name || 'Гость';
    userId.value = tg.initDataUnsafe.user.id;
  }
});

const showUserId = () => {
  alert(`Ваш ID: ${userId.value}`);
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