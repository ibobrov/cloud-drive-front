<template>
  <div v-for="folder in folders" :key="folder.id" class="bg-gray-200 p-4 rounded-lg shadow-md min-h-32 flex items-center justify-center">
    <h2 class="text-xl font-bold">
      {{ folder.name }}
    </h2>
  </div>

  <div class="bg-blue-500 text-white p-2 rounded min-h-32 flex items-center justify-center">
    <button @click="showModal">Добавить папку</button>

    <div v-if="isModalVisible" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-blue-600 p-6 rounded-lg shadow-lg">
        <h2 class="text-xl font-bold mb-4">Добавить новую папку</h2>
        <input type="text" v-model="folderName" class="border p-2 w-full text-stone-950 mb-4" placeholder="Введите имя новой папки">
        <div class="flex justify-end">
          <button @click="hideModal" class="bg-gray-500 text-white p-2 rounded mr-2">Отмена</button>
          <button @click="saveFolder" class="bg-green-500 text-white p-2 rounded">Сохранить</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
  },
  data() {
    return {
      isModalVisible: false,
      folderName: '',
      folders: []
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },

    hideModal() {
      this.isModalVisible = false;
    },

    loadFolders() {
      fetch('http://localhost/api/folders', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
          'Origin': 'http://localhost:5173'
        }
      })
          .then(response => response.json())
          .then(data => {
            this.folders = data; // Предполагаем, что сервер возвращает массив папок
            console.log(this.folders)
          })
          .catch(error => console.error('Ошибка:', error));
    },

    saveFolder() {
      if (this.folderName) {
        fetch('http://localhost/api/folders', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Origin': 'http://localhost:5173'
          },
          body: JSON.stringify({ name: this.folderName })
        })
        .then(response => response.json())
        .then(data => {
          if (data) {
            this.folders.push({ id: data.id, name: data.name });
            this.folders.sort((a, b) => a.name.localeCompare(b.name));
            this.folderName = null
            this.hideModal();
          } else {
            alert('Ошибка при добавлении папки.');
          }
        })
        .catch(error => console.error('Ошибка:', error));
      }
    }
  },
  mounted() {
    this.loadFolders();
  }
};
</script>

<style scoped>
/* Добавьте стили, если необходимо */
</style>