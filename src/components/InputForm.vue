<template>
    <div class="input-container">
      <input
        :value="newName" 
        @input="$emit('update-new-name', $event.target.value)"
        placeholder="Escribe un nombre"
        @keyup.enter="$emit('add-name')"
      />
      <button @click="$emit('add-name')">Registrar</button>
    </div>
  </template>
  
  <script>
  export default {
    name: "InputForm",
    props: ["newName", "addName"],
  };
  </script>
  
  <style scoped>
  .input-container {
    display: flex;
    gap: 15px;
    margin-bottom: 25px;
  }
  input {
    flex: 1;
    padding: 15px;
    border: 1px solid #444;
    border-radius: 8px;
    background-color: #333;
    color: #e0e0e0;
  }
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
  