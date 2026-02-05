<script>
import ActionButtons from "./components/ActionButtons.vue";
import PlayerPanel from "./components/PlayerPanel.vue";
import StatusMessage from "./components/StatusMessage.vue";

import playerImg from "../public/good.png";
import enemyImg from "../public/evil.png";

export default {
  components: {
    ActionButtons,
    PlayerPanel,
    StatusMessage,
  },

  methods: {
    attackLight() {
      if (this.playerHp <= 0 || this.enemyHp <= 0) {
        return;
      }
      this.enemyHp -= 10;
      this.statusMessage = "Vous avez infligé 10 dégâts à l'ennemi !";
      if (this.enemyHp <= 0) {
        this.enemyHp = 0;
        this.statusMessage = "Vous avez gagné !";
        this.isGameOver = true;
      } else {
        this.enemyTurn();
      }
    },
    getEnemyDamage() {
      if (this.difficulty === "easy") {
        return Math.floor(Math.random() * 8) + 3; // 3 à 10
      }
      if (this.difficulty === "normal") {
        return Math.floor(Math.random() * 15) + 5; // 5 à 20
      }
      if (this.difficulty === "hard") {
        return Math.floor(Math.random() * 20) + 10; // 10 à 30
      }
    },
    enemyTurn() {
      const damage = this.getEnemyDamage();
      this.playerHp -= damage;
      this.statusMessage += ` L'ennemi vous a infligé ${damage} dégâts !`;
      if (this.playerHp <= 0) {
        this.playerHp = 0;
        this.statusMessage = "Vous avez perdu !";
        this.isGameOver = true;
      }
    },
    attackHeavy() {
      if (this.playerHp <= 0 || this.enemyHp <= 0) {
        return;
      }
      this.enemyHp -= 20;
      this.statusMessage = "Vous avez infligé 20 dégâts à l'ennemi !";
      if (this.enemyHp <= 0) {
        this.enemyHp = 0;
        this.statusMessage = "Vous avez gagné !";
        this.isGameOver = true;
      } else {
        this.enemyTurn();
      }
    },
    heal() {
      if (this.playerHp <= 0 || this.enemyHp <= 0) {
        return;
      }
      if (this.playerHp <= 0 || this.enemyHp <= 0) {
        return;
      }
      this.playerHp += 10;
      this.statusMessage = "Vous avez été soigné de 10 points de vie !";
      if (this.playerHp > this.maxHp) {
        this.playerHp = this.maxHp;
      }
      if (this.enemyHp <= 0) {
        this.enemyHp = 0;
        this.statusMessage = "Vous avez gagné !";
        this.isGameOver = true;
      } else {
        this.enemyTurn();
      }
    },


    resetGame() {
      this.playerHp = 100;
      this.enemyHp = 100;
      this.statusMessage = "Commencer le combat !";
      this.isGameOver = false;
    },
  },

  data() {
    return {
      playerHp: 100,
      enemyHp: 100,
      statusMessage: "Commencer le combat !",
      isGameOver: false,
      maxHp: 100,
      difficulty: "normal",

      playerImg,
      enemyImg
    };
  },
};
</script>

<template>
  <header>
    <h1>Jeu de combat</h1>
  </header>
  <main>
    <div class="difficulty">
      <label>Choisir la difficulté :</label>
      <select v-model="difficulty">
        <option value="easy">Facile</option>
        <option value="normal">Normal</option>
        <option value="hard">Difficile</option>
      </select>
    </div>

    <div class="player-panels">
      
      <PlayerPanel name="Joueur" :hp="playerHp" :maxHp="maxHp" :img="playerImg" />
      <PlayerPanel name="Ennemi" :hp="enemyHp" :maxHp="maxHp" :img="enemyImg" />
    </div>

    <ActionButtons
      @attack-light="attackLight"
      @attack-heavy="attackHeavy"
      @heal="heal"
    />

    <StatusMessage :message="statusMessage" />

    <button @click="resetGame">Rejouer</button>
  </main>
</template>

<style scoped>
main {
  background: #9bbc0f;
  border: 4px solid #0f380f;
  padding: 20px;
  width: 60%;
  margin: 30px auto;
  box-shadow: 0 0 0 6px #0f380f;
  font-family: "Press Start 2P", monospace;
  color: #0f380f;
}

header h1 {
  text-align: center;
  font-size: 16px;
  color: #0f380f;
  text-transform: uppercase;
  margin-bottom: 20px;
  font-family: "Press Start 2P", monospace;
}

/* Bouton Rejouer */
button {
  background: #8bac0f;
  color: #0f380f;
  border: 3px solid #0f380f;
  padding: 12px;
  font-family: "Press Start 2P", monospace;
  font-size: 12px;
  cursor: pointer;
  text-transform: uppercase;
  transition:
    transform 0.1s,
    background 0.2s;
  box-shadow: 0 0 0 4px #0f380f;
  width: 20%;
  margin-top: 20px;
}

button:hover {
  background: #9bbc0f;
  transform: translateY(-3px);
}

button:active {
  transform: translateY(0px);
  background: #306230;
}

.player-panels {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.difficulty {
  margin-bottom: 20px;
  text-align: center;
  font-family: "Press Start 2P", monospace;
  color: #0f380f;
}

select {
  background: #8bac0f;
  border: 3px solid #0f380f;
  padding: 8px;
  font-family: "Press Start 2P", monospace;
  color: #0f380f;
  cursor: pointer;
  box-shadow: 0 0 0 4px #0f380f;
}

</style>
