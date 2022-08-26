<script setup>
  import { ref } from 'vue';

  const themeDark = ref('');

  if (
    localStorage.theme === 'dark' ||
    (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
  ) {
    document.documentElement.classList.add('dark');
    themeDark.value = '🌞';
  } else {
    document.documentElement.classList.remove('dark');
    themeDark.value = '🌚';
  }

  const handleDarkMode = () => {
    document.documentElement.classList.toggle('dark');
    if (document.documentElement.classList.contains('dark')) {
      localStorage.theme = 'dark';
      themeDark.value = '🌞';
    } else {
      localStorage.theme = 'light';
      themeDark.value = '🌚';
    }
  };
</script>

<template>
  <main
    class="bg-slate-100 min-h-screen font-mono flex justify-center items-center dark:bg-slate-800 transition-colors"
  >
    <section class="container mx-auto w-full h-full text-center">
      <h1 class="text-5xl mb-5 text-slate-900 dark:text-slate-100 transition-colors">Dark Mode</h1>
      <button
        class="text-lg text-slate-700 hover:text-slate-900 py-2 px-6 rounded-md border-2 border-slate-700 hover:border-slate-900 hover:shadow-lg dark:text-slate-50 dark:hover:text-slate-200 dark:border-slate-50 dark:hover:border-slate-200 dark:hover:shadow-gray-900 transition-all"
        @click="handleDarkMode"
      >
        {{ themeDark }}
      </button>
    </section>
  </main>
</template>
