<template>
    <div class="list-container">
      <ul>
        <li
          v-for="(name, index) in names"
          :key="index"
          :class="{ selected: selectedIndexes.includes(index) }"
          @click="toggleSelection(index)"
        >
          <div class="list-item">
            <span v-if="editingIndex !== index">{{ name }}</span>
            <template v-if="editingIndex === index">
              <input
                :value="localEditedName"
                @input="$emit('update-edited-name', $event.target.value)"
                @keyup.enter="$emit('save-edit', index)"
                @blur="$emit('save-edit', index)"
                class="edit-input"
              />
            </template>
            <button
              v-if="editingIndex !== index"
              @click.stop="startEditing(index, name)"
            >
              Editar
            </button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: "NameList",
    props: [
      "names",
      "selectedIndexes",
      "toggleSelection",
      "editingIndex",
      "editedName",
    ],
    data() {
      return {
        localEditedName: "",
      };
    },
    methods: {
      startEditing(index, currentName) {
        this.$emit("start-editing", index);
        this.localEditedName = currentName;
      },
    },
  };
  </script>
  
  <style scoped>
  .list-container {
    background-color: #2b2b2b;
    padding: 20px;
    border-radius: 15px;
    box-shadow: inset 0 0 5px rgba(46, 204, 113, 0.5);
    max-height: calc(5 * 60px);
    overflow-y: auto;
    scrollbar-width: thin;
    scrollbar-color: #2ecc71 #2b2b2b;
  }
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  li {
    margin-bottom: 8px;
    padding: 12px;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  li.selected {
    background-color: #555;
  }
  
  .list-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .list-item button {
    background-color: #444;
    color: #e0e0e0;
    padding: 8px 12px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .list-item button:hover {
    background-color: #777;
  }
  
  .edit-input {
    flex: 1;
    padding: 8px;
    border: 1px solid #2ecc71;
    border-radius: 5px;
    background-color: #333;
    color: #e0e0e0;
  }
  </style>
  