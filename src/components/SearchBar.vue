<template>
  <div class="search-bar flex items-center bg-gray-200 py-2 px-4 rounded-md shadow-md">
    <input
      type="text"
      placeholder="Search..."
      class="flex-grow py-2 px-4 bg-white rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
      @input="handleInput"
    />
    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 19l-6-6M12 6l6 6" />
    </svg>
  </div>
  </template>
  
  <script>
  export default {
    methods: {
      handleInput(event) {
        const searchText = event.target.value;
        this.$emit('search', searchText);
      },
    },
  };
  </script>
  
  <style scoped>
  .search-bar {
  width: 100%;
}

.input {
  width: 100%;
}
  /* Add custom styles if needed */
  </style>
  