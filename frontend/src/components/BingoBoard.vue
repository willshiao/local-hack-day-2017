<template>
  <div class="hello">
    <audio id="myAudio">
      <source src="/static/win.mp3" type="audio/mpeg">
      Your browser does not support the audio element.
    </audio>
    <h1 class="title">ACM Bingo Board</h1>
    <div class="tile-collection"
      :class="{win : isWinning}">
      <div
        class="tile"
        v-for="t in terms"
        :key="t.name"
        :class="{ active : t.isActive }"
        @click="toggleTile(t)"
      >
        <p class="tile-value">{{ t.name }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.win {
  background-color: green;
}
.title {
  text-align: center;
}
.tile-collection {
  display: flex;
  flex-wrap:wrap;
  margin: 0 auto;
  align-items: center;
  justify-content: center;
}
.hello {
  height: 100%;
  width: 100%;
}
.tile {
  width: calc(100% * (1/5) - 10px + 5px);
  height: 20vw;
  background-color: #0972b3;
  color: white;
  text-align: center;
  font-size: 3vw;
  border: #0951a2 1px solid;
  vertical-align: middle;
}
@media (min-width: 750px) {
  .tile-collection {
    width: 50%;
  }
  .tile {
    width: 9vw;
    height: 9vw;
    font-size: 1vw;
  }
}

.active {
  background-color: #e20000;
}
.tile-value {
  position: relative;
  top: 30%;    
  left: 0;
  width: 100%;
}
</style>

<script>
import axios from 'axios'
export default {
  name: 'BingoBoard',
  methods: {
    toggleTile (t) {
      t.isActive = !t.isActive
      this.checkBoard()
    },
    checkBoard () {
      if ((this.terms[0].isActive &&
        this.terms[1].isActive &&
        this.terms[2].isActive &&
        this.terms[3].isActive &&
        this.terms[4].isActive) ||
        (this.terms[0].isActive &&
        this.terms[5].isActive &&
        this.terms[10].isActive &&
        this.terms[15].isActive &&
        this.terms[20].isActive) ||
        (this.terms[0].isActive &&
        this.terms[6].isActive &&
        this.terms[12].isActive &&
        this.terms[18].isActive &&
        this.terms[24].isActive) ||
        (this.terms[5].isActive &&
        this.terms[6].isActive &&
        this.terms[7].isActive &&
        this.terms[8].isActive &&
        this.terms[9].isActive) ||
        (this.terms[10].isActive &&
        this.terms[11].isActive &&
        this.terms[12].isActive &&
        this.terms[13].isActive &&
        this.terms[14].isActive) ||
        (this.terms[15].isActive &&
        this.terms[16].isActive &&
        this.terms[17].isActive &&
        this.terms[18].isActive &&
        this.terms[19].isActive) ||
        (this.terms[20].isActive &&
        this.terms[21].isActive &&
        this.terms[22].isActive &&
        this.terms[23].isActive &&
        this.terms[24].isActive) ||
        (this.terms[1].isActive &&
        this.terms[6].isActive &&
        this.terms[11].isActive &&
        this.terms[16].isActive &&
        this.terms[21].isActive) ||
        (this.terms[2].isActive &&
        this.terms[7].isActive &&
        this.terms[12].isActive &&
        this.terms[17].isActive &&
        this.terms[22].isActive) ||
        (this.terms[3].isActive &&
        this.terms[8].isActive &&
        this.terms[13].isActive &&
        this.terms[18].isActive &&
        this.terms[23].isActive) ||
        (this.terms[4].isActive &&
        this.terms[9].isActive &&
        this.terms[14].isActive &&
        this.terms[19].isActive &&
        this.terms[24].isActive) ||
        (this.terms[4].isActive &&
        this.terms[8].isActive &&
        this.terms[12].isActive &&
        this.terms[16].isActive &&
        this.terms[20].isActive)) {
        this.isWinning = true
        document.getElementById('myAudio').play()
      } else {
        this.isWinning = false
      }
      return true
    }
  },
  created () {
    axios.get('http://www.json-generator.com/api/json/get/cfpbdLwCsy?indent=2')
      .then((res) => {
        this.terms = res.data
      })
  },
  data () {
    return {
      isWinning: false,
      terms: []
    }
  }
}
</script>