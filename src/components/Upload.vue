<template>
  <div
    :class="[{ 'drag-enter': isDragEntered }, { 'invalid-drop': isInvalidDrop }, 'upload-drop']"
    @dragenter="$emit('drag-enter', $event)"
    @dragover="$emit('drag-enter', $event)"
    @dragleave="$emit('drag-leave', $event)"
    @drop="$emit('drop', $event)"
  >
    <div>Upload Excel File</div>

    <div v-if="fileName" class="file-name">{{fileName}}</div>
    <input
      type="file"
      ref="file"
      @change="$emit('handle-file-picker', $event)"
      style="visibility: hidden"
    />
    <button class="select-file-button" @click="$refs.file.click()">Select a file</button>
  </div>
</template>

<script>
export default {
  name: "Upload",
  props: {
    isDragEntered: Boolean,
    isInvalidDrop: Boolean,
    fileName: String
  }
};
</script>

<style scoped>
.upload-drop {
  width: 200px;
  padding: 40px;
  border: 1px dashed lightblue;
  border-radius: 2px;
  background-color: white;
}

.file-name {
  font-size: 0.8em;
  font-weight: 700;
  color: rgb(79, 93, 112);
  padding-top: 10px;
}

.select-file-button {
  background-color: lightgray;
  padding: 10px;
  border-radius: 2px;
}

.drag-enter {
  background-color: lightblue;
}

.invalid-drop {
  cursor: not-allowed;
  background-color: white;
  border: 1px solid lightcoral;
}
</style>