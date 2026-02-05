<template>
  <div class="player-panel">
    <h2 class="player-name">{{ name }}</h2>

    <img :src="img" alt="représentation du perso">

    <div class="hp-container">
      <div class="hp-bar">
        <div class="hp-fill" :style="{ width: (hp / maxHp * 100) + '%' }"></div>
      </div>
      <p class="hp-text">{{ hp }} / {{ maxHp }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PlayerPanel",
  props: {
    name: {
      type: String,
      required: true
    },
    hp: {
      type: Number,
      required: true
    },
    maxHp: {
      type: Number,
      required: true
    },
    img: {
      type: String,
      required: false
    }
  }
}
</script>


<style scoped>
.player-panel {
  background: #1b1b1b;
  border: 3px solid #ffffff;
  padding: 15px;
  width: 220px;
  font-family: "Press Start 2P", monospace;
  color: #ffffff;
  margin-bottom: 20px;
  text-align: center;
}

.player-name {
  font-size: 14px;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.hp-container {
  margin-top: 10px;
}

.hp-bar {
  width: 100%;
  height: 18px;
  background: #444;
  border: 2px solid #fff;
  position: relative;
}

.hp-fill {
  height: 100%;
  background: #4caf50;
  transition: width 0.3s;
}

.hp-text {
  margin-top: 5px;
  font-size: 12px;
}

img {
  width: 80px;
  height: 80px;
  margin-bottom: 10px;
}
</style>
