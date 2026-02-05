<template>
    <div class="dialog-box">
    <p class="dialog-message">{{ message }}</p>
    </div>
</template>

<script>
export default {
  name: "StatusMessage",
  props: {
        message: {
      type: String,
      required: true
    }
  }
  }

</script>

<style scoped>
.dialog-box {
  background: #1b1b1b;
  border: 4px solid #ffffff;
  padding: 15px;
  margin: 20px auto;
  font-family: "Press Start 2P", monospace;
  color: #ffffff;
  box-shadow: 0 0 0 4px #000000;
  width: 80%;
}

.dialog-text {
  font-size: 14px;
  line-height: 1.6;
  white-space: pre-line;
}
</style>