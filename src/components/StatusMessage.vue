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
/* optionnel */
</style>