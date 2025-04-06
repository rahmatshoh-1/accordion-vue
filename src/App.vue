<script setup>
import { ref } from 'vue';

const active = ref(false);
const questions = ref([
  {
    id: 1,
    question: "Как правильно подбирать шрифты и цвета?",
    answer: "Используйте не более 2–3 гарнитур. Google Fonts — хороший ресурс. Подбирайте палитру на Coolors или Adobe Color. Проверяйте контрастность для доступности (например, через WebAIM Contrast Checker).",
    isOpen: false
  },
  {
    id: 2,
    question: "Что такое адаптивная вёрстка?",
    answer: "Это подход, при котором сайт корректно отображается на всех устройствах (ПК, планшеты, смартфоны). Основные инструменты: медиазапросы (@media), относительные единицы (rem, %, vw), Flexbox/Grid для гибких макетов.",
    isOpen: false
  },
  {
    id: 3,
    question: "Как проверять вёрстку на ошибки?",
    answer: "1. Валидатор HTML/CSS: W3C Validator. 2. Доступность: Lighthouse в Chrome DevTools. 3. Кроссбраузерность: проверяйте в Chrome, Firefox, Safari, Edge. 4. Pixel Perfect: сравнение с макетом через расширения типа PerfectPixel.",
    isOpen: false
  },
  {
    id: 4,
    question: "Что такое CSS-препроцессоры (Sass/Less)?",
    answer: "Это инструменты, расширяющие возможности CSS. Например, Sass позволяет: использовать переменные ($primary-color), вложенность селекторов, миксины для повторяющегося кода, модульность (@import). Компилируются в обычный CSS.",
    isOpen: false
  }
]);
const toggleAnswer = function (id) {
  questions.value = questions.value.map(question => {
    if (question.id === id) {
      return { ...question, isOpen: !question.isOpen }; // инвертируем состояние
    }
    return { ...question, isOpen: false };
  });
}
</script>

<template>
  <header class="bg-green-main h-[280px]"></header>
  <main class="relative mx-4">
    <div class="rounded-md absolute left-0 right-0 m-auto -top-40  z-10 bg-white shadow-2xl max-w-[600px] p-8">
      <div class="flex items-center text-green-main ">
        <img src="/images/logo.svg" alt="logo">
        <div class="flex items-center">
          <h1 class="text-desktop-preset-1 font-black ">ЧЗВ</h1>
          <span class="leading-4 ml-2">Часто задаваемые<br> вопросы</span>
        </div>
      </div>

      <div v-for="question in questions" :key="question.id" class="border-t py-5 border-gray-200">
        <div class="flex gap-8 justify-between items-start cursor-pointer" @click="toggleAnswer(question.id)">
          <h2 class="sm:text-mobile-preset-2 md:text-tablet-preset-2 lg:text-desktop-preset-2 font-bold text-green-main">{{ question.question }}</h2>
          <button :aria-label="question.isOpen ? 'Скрыть ответ' : 'Показать ответ'" class="cursor-pointer mt-3 bg-green-main rounded-full flex-none">
            <img v-if="question.isOpen" src="/images/minus.svg" alt="Icon minus">
            <img v-else src="/images/plus.svg"  alt="Icon Plus" >
          </button>
        </div>
        <p v-if="question.isOpen"  class="mt-5 text-green-secondary sm:text-mobile-preset-3 md:text-tablet-preset-3 lg:text-desktop-preset-3">
          {{ question.answer }}
        </p>

      </div>
    </div>
  </main>
</template>
