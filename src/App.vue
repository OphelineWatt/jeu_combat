<script>
import ActionButtons from "./components/ActionButtons.vue";
import PlayerPanel from "./components/PlayerPanel.vue";
import StatusMessage from "./components/StatusMessage.vue";

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
  enemyTurn() {
    const damage = Math.floor(Math.random() * 15) + 5; 
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
  }
},

  data() {
  return {
    playerHp: 100,
    enemyHp: 100,
    statusMessage: "Commencer le combat !",
    isGameOver: false,
    maxHp: 100
  }
}
};
</script>

<template>
  <header>
    <h1>Jeu de combat</h1>
  </header>
  <main>
    <PlayerPanel name="Joueur" :hp="playerHp" :maxHp="maxHp" />
    <PlayerPanel name="Ennemi" :hp="enemyHp" :maxHp="maxHp" />

    <ActionButtons @attack-light="console.log('attaque légère')" @attack-heavy="console.log('attaque lourde')" @heal="console.log('soin')" />

    <StatusMessage :message="statusMessage" />

    <button>Rejouer</button>
  </main>
</template>

<style scoped></style>
