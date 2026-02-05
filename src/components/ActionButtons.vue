<template>
  <button @click="$emit('attack-light')">attaque légère</button>
  <button @click="$emit('attack-heavy')">attaque lourde</button>
  <button @click="$emit('heal')">soin</button>
</template>

<script>
export default {
  name: "ActionButtons",
  props: {

}
}
</script>

<style scoped>
/* optionnel */
</style>