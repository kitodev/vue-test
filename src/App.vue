<template>
  <div>
    <button class="toggle-button" @click="toggleOverlay">Toggle Overlay</button>
    <div v-if="randomItem">
    <div class="overlay" :class="{ active: overlayActive }">
    <div class="in">
    <div class="talents" v-for="talent of talents">
    <h2>{{ talent.name }} </h2>
        <div class="talent">
          <div class="date">{{ talent.from }} - {{ talent.to }}</div>
          <div class="talent-description">
            <div class="box">{{ talent.talent.join(', ')}}</div>
          </div>
        </div>
      </div>
      </div>
  </div>
  </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      overlayActive: false,
      currentEvent: '',
      talents: [],
      randomItem: [],
    }
  },
  methods: {
    toggleOverlay() {
        fetch("http://localhost:3000/data")
          .then(response => response.json())
          .then(data => {
            this.talents = data;
            const randomIndex = Math.floor(Math.random() * this.talents.length);
            this.randomItem = this.talents[randomIndex];
            console.log(this.randomItem);
          })
      }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  margin-top: 60px;
}

$font-size: 1.5rem;
$line-height: 2rem;
$padding: 2rem;


.toggle-button {
  position: absolute;
  top: $padding;
  right: $padding;
}

.talents {
  h2 {
    color: white;
     text-shadow: 2px 2px #000;
     text-transform: uppercase;
  }
  width: 100%;
  display: flex;
  background: #00d487;
  flex-direction: column;
  border-radius: 20px;
  justify-content: space-between;
  border: 5px solid black;

  .date {
    padding: 15px 0px;
    background: #fff;
    font-weight: 400;
    color: #000;
    border-top: 5px solid #000;
    border-bottom: 5px solid #000;
  }
}

.talent-description {
  display: flex;
  justify-content: space-between;
  flex: 1;

  .box {
    width: 100%;
    font-size: 18px;
    color: white;
    text-shadow: 2px 2px #000;
    padding: 20px 20px;

    &:nth-last-child(2) {
    border-right: 3px solid #000;
    border-left: 3px solid #000;
    }
  }
}

.overlay {
  width: 100%;
  max-width: 1920px;
  height: 950px;
  margin: 0 15px;
  border-radius: 20px;
  .in {
    border: 2px solid  white;
    display: flex;
    border-radius: 20px;
  }
}
</style>
