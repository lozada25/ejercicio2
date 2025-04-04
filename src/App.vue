<template>
  <div class="app">
    <Title />
    <InputForm
      :newName="newName"
      @update-new-name="updateNewName"
      @add-name="addName"
    />
    <NameList
      :names="names"
      :selectedIndexes="selectedIndexes"
      :toggleSelection="toggleSelection"
      :editingIndex="editingIndex"
      @start-editing="startEditing"
      @save-edit="saveEdit"
    />
    <DeleteButton
      :removeSelected="removeSelected"
      :selectedIndexes="selectedIndexes"
    />
  </div>
</template>

<script>
import Title from "./components/Title.vue";
import InputForm from "./components/InputForm.vue";
import NameList from "./components/NameList.vue";
import DeleteButton from "./components/DeleteButton.vue";

export default {
  name: "App",
  components: {
    Title,
    InputForm,
    NameList,
    DeleteButton,
  },
  data() {
    return {
      newName: "",
      names: [],
      selectedIndexes: [],
      editingIndex: null,
    };
  },
  methods: {
    updateNewName(value) {
      this.newName = value;
    },
    addName() {
      if (this.newName.trim()) {
        this.names.push(this.newName.trim());
        this.newName = "";
      }
    },
    toggleSelection(index) {
      const selected = this.selectedIndexes.includes(index);
      if (selected) {
        this.selectedIndexes = this.selectedIndexes.filter((i) => i !== index);
      } else {
        this.selectedIndexes.push(index);
      }
    },
    removeSelected() {
      this.names = this.names.filter(
        (_, index) => !this.selectedIndexes.includes(index)
      );
      this.selectedIndexes = [];
    },
    startEditing(index) {
      this.editingIndex = index;
    },
    saveEdit(index, newName) {
      if (newName.trim()) {
        this.names[index] = newName.trim();
      }
      this.editingIndex = null;
    },
  },
};
</script>

<style scoped>
.app {
  font-family: Arial, sans-serif;
  width: 600px;
  background-color: #1e1e1e; 
  color: #e0e0e0;
  padding: 30px;
  border-radius: 15px;
  border: 3px solid #2ecc71; 
  box-shadow: 0 4px 8px rgba(46, 204, 113, 0.8); 
  position: absolute; 
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>

