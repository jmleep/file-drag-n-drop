<template>
  <div class="upload-container">
    <upload
      @drag-enter="dragEnter"
      @drag-leave="dragLeave"
      @drop="drop"
      @handle-file-picker="handleFilePicker"
      :isDragEntered="isDragEntered"
      :isInvalidDrop="isInvalidDrop"
      :fileName="fileName"
    />
    <div v-if="isInvalidDrop" class="invalid-drop-error">
      <div>One file permitted at a time</div>
    </div>
    <submit-button :conditional="excelData !== null" @submit="submitFile" />
  </div>
</template>

<script>
import Upload from "./Upload";
import SubmitButton from "./SubmitButton";

export default {
  name: "UploadContainer",
  components: {
    Upload,
    SubmitButton
  },
  data: () => {
    return {
      isDragEntered: false,
      isInvalidDrop: false,
      excelData: null,
      fileName: "No File Selected",
      file: null
    };
  },
  methods: {
    dragEnter(event) {
      event.preventDefault();
      this.isDragEntered = true;
      this.isInvalidDrop = event.dataTransfer.items.length > 1 ? true : false;
    },
    dragLeave(event) {
      event.preventDefault();
      this.isDragEntered = false;
      this.isInvalidDrop = false;
    },
    drop(event) {
      event.preventDefault();
      this.isDragEntered = false;
      this.isInvalidDrop = false;
      const { files } = event.dataTransfer;

      if (files.length === 1) {
        const file = files[0];
        this.file = file;
        this.fileName = file.name;
        this.processFile();
      }
    },
    processFile() {
      const fileReader = new FileReader();

      fileReader.onload = event => {
        const { result } = event.target;
        this.excelData = result;
      };

      fileReader.readAsText(this.file);
    },
    handleFilePicker(event) {
      this.file = event.target.files[0];
      this.fileName = this.file.name;
      this.processFile();
    },
    submitFile() {
      console.log(this.fileName);
    }
  }
};
</script>

<style scoped>
.upload-container {
  display: flex;
  align-items: center;
  flex-flow: column wrap;
  justify-content: space-around;
}

.invalid-drop-error {
  padding: 3px;
  margin-top: 5px;
  background-color: lightcoral;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 2px;
  font-size: 0.85em;
}
</style>