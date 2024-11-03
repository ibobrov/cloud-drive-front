<script setup>
import FolderComponent from "@/components/FolderComponent.vue";
</script>

<template>
  <div class="flex-container">
  <header class="bg-yellow-500 p-4 shadow-md">
    <h1 class="text-2xl text-center text-white font-bold">Google Drive Killer</h1>
  </header>

  <div class="container mx-auto p-12 content">
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4">
      <FolderComponent/>
    </div>
  </div>

  <footer class="bg-red-500 p-4 shadow-md text-center">
    <a href="https://github.com/ibobrov" class="text-white font-bold">GitHub: ibobrov</a>
  </footer>
  </div>
</template>

<style>
  body, html {
    height: 100%;
    margin: 0;
  }

  .flex-container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  .content {
    flex: 1;
  }
</style>
