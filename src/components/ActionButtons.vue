<template>
    <div class="buttons">
  <button @click="$emit('attack-light')">attaque légère</button>
  <button @click="$emit('attack-heavy')">attaque lourde</button>
  <button @click="$emit('heal')">soin</button>
</div>
</template>

<script>
export default {
  name: "ActionButtons",
  props: {

}
}
</script>

<style scoped>
.buttons {
  display: flex;
  flex-direction: row;
  gap: 12px;
  width: 220px;
  margin: 20px auto;
  justify-content: space-between;
}

button {
  background: #1b1b1b;
  color: #ffffff;
  border: 3px solid #ffffff;
  padding: 12px;
  font-family: "Press Start 2P", monospace;
  font-size: 12px;
  cursor: pointer;
  text-transform: uppercase;
  transition: transform 0.1s, background 0.2s;
  box-shadow: 0 0 0 4px #000000;
}

button:hover {
  background: #333333;
  transform: translateY(-3px);
}

button:active {
  transform: translateY(0px);
  background: #555555;
}
</style>