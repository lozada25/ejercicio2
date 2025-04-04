<template>
    <button @click="removeSelected" :disabled="!selectedIndexes.length">
      Eliminar Seleccionados
    </button>
  </template>
  
  <script>
  export default {
    name: "DeleteButton",
    props: ["removeSelected", "selectedIndexes"],
  };
  </script>
  
  <style scoped>
  button {
    padding: 15px 20px;
    border: none;
    border-radius: 8px;
    background-color: #555;
    color: #e0e0e0;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  button:hover {
    background-color: #777;
  }
  button:disabled {
    background-color: #444;
    cursor: not-allowed;
  }
  </style>
  