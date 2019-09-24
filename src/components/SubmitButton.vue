<template>
  <div v-if="conditional" class="button-wrapper">
    <button class="submit-button" @click="$emit('submit', $event)">Submit</button>
  </div>
</template>

<script>
export default {
  name: "SubmitButton",
  props: {
    conditional: Boolean
  }
};
</script>

<style scoped>
.button-wrapper {
  margin-top: 10px;
}

.submit-button {
  background-color: lightseagreen;
  color: white;
  padding: 10px;
  width: 200px;
  border-radius: 2px;
}
</style>
