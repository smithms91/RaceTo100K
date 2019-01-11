<template>
  <div id="app">
    <h1 class="title"><span>Race to</span><br />100,000</h1>
    <div class="kills">
      <p>{{ninja_kills}}</p>
      <p class="vs">&nbsp;VS&nbsp;</p>
      <p>{{hd_kills}}</p>
    </div>
    <div class="stats">
      <div class="ninja_stats">
        <h1>Ninja</h1>
        <h4>Wins: <span class="large_number">{{ninja_wins}}</span></h4>
        <h4>Win Percent: <span class="large_number">{{ninja_win_percent}}</span></h4>
        <h4>K/D: <span class="large_number">{{ninja_kd}}</span></h4>
      </div>
      <div class="hd_stats">
        <h1>HD</h1>
        <h4>Wins: <span class="large_number">{{hd_wins}}</span></h4>
        <h4>Win Percent: <span class="large_number">{{hd_win_percent}}</span></h4>
        <h4>K/D: <span class="large_number">{{hd_kd}}</span></h4>
      </div>
    </div>
    <div class="pcspecs">
      <h4>PC Specs</h4>
      <div class="line"></div>
      <div class="specs">
        <div class="ninja">
          <ul>
            <li><a href="https://amzn.to/2M3u3EN">FINALMOUSE AIR58</a></li>
            <li><a href="https://amzn.to/2SNwC0b">CORSAIR K70 RGB MK.2</a></li>
            <li><a href="https://amzn.to/2D2MdUa">INTEL CORE I9-9900K</a></li>
            <li><a href="https://amzn.to/2SQDFoH">ASUS ROG MAXIMUS XI HERO</a></li>
            <li><a href="https://amzn.to/2SPaOBt">G.SKILL TRIDENTZ RGB 32GB</a></li>
            <li><a href="https://amzn.to/2D5z90t">NVIDIA RTX 2080 TI</a></li>
            <li><a href="https://amzn.to/2RnNca7">SEAGATE BARRACUDA 4TB (2)</a></li>
          </ul>
        </div>
        <div class="center">
          <ul>
            <li>Mouse</li>
            <li>Keyboard</li>
            <li>CPU</li>
            <li>Motherboard</li>
            <li>RAM</li>
            <li>Graphics Card</li>
            <li>HDD</li>
          </ul>
        </div>
        <div class="hd">
          <ul>
            <li><a href="https://amzn.to/2M5uv5l">LOGITECH G502 HERO</a></li>
            <li><a href="https://amzn.to/2FozP2e">LOGITECH G PRO</a></li>
            <li><a href="https://amzn.to/2RHjSe3">INTEL CORE I7-7800X</a></li>
            <li><a href="https://amzn.to/2M7wRAs">ASUS TUF X299 MARK 2</a></li>
            <li><a href="https://amzn.to/2SPaOBt">G.SKILL TRIDENTZ RGB 32GB</a></li>
            <li><a href="https://amzn.to/2RLX0dm">MSI GEFORCE GTX 1080</a></li>
            <li><a href="https://amzn.to/2RnNca7">SEAGATE BARRACUDA 4TB (2)</a></li>
          </ul>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      "hd_kills": "33333",
      "hd_wins": "2323",
      "hd_win_percent": "32",
      "hd_kd": "3",
      "hdStats": "",
      "ninja_kills": "44444",
      "ninja_wins": "3232",
      "ninja_win_percent": "32",
      "ninja_kd": "4",
      "ninjaStats": ""
    }
  },
  name: 'app',
  methods: {
    ninjaData() {
      axios.post(`http://localhost:3000/fortnite`, {
        epicUsername: "ninja"
      }).then((response) => {
        this.ninjaStats = response.data;
        this.ninja_kills = this.ninjaStats.lifeTimeStats[10].value
        this.ninja_win_percent = this.ninjaStats.lifeTimeStats[9].value
        this.ninja_wins = this.ninjaStats.lifeTimeStats[8].value
        this.ninja_kd = this.ninjaStats.lifeTimeStats[11].value
      }).catch((error) => {
        console.log(error);
      })
    },
    hdData() {
      axios.post(`http://localhost:3000/fortnite`, {
        epicUsername: "highdistortion"
      }).then((response) => {
        this.hdStats = response.data;
        this.hd_kills = this.hdStats.lifeTimeStats[10].value
        this.hd_win_percent = this.hdStats.lifeTimeStats[9].value
        this.hd_wins = this.hdStats.lifeTimeStats[8].value
        this.hd_kd = this.hdStats.lifeTimeStats[11].value
      }).catch((error) => {
        console.log(error);
      })
    }
  },
  beforeMount() {
    this.ninjaData()
    this.hdData()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Luckiest+Guy');
@import url('https://fonts.googleapis.com/css?family=PT+Sans');

* {
  margin: 0;
  padding: 0;
  outline: none;
  box-sizing: border-box;
}

#app {
  background-image: url("./assets/ninjahd.png");
  width: 100%;
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  color: white;
  padding-top: 50px;
  font-family: "PT Sans", sans-serif;
}

h1 {
  font-size: 80px;
  font-family: "PT Sans", sans-serif;
  text-transform: uppercase;
}

.title {
  text-align: center;
  font-family: 'PT Sans', sans-serif;
}

.title span {
  font-size: 60px;
}

h4 {
  font-size: 25px;
}

.kills {
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Luckiest Guy', sans-serif;
  font-size: 150px;
  margin: 50px 0;
}

.vs {
  font-size: 50px;
  margin: 0 30px;
}

.pcspecs {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 200px;
  position: fixed;
  bottom: 150px;
  z-index: 1555;
}

.specs {
  display: flex;
  justify-content: space-around;
  text-align: center;
  width: 650px;
  margin-top: 20px;
}

.specs ul {
  list-style-type: none;
}

.specs ul a {
  color: lightblue;
}

.center {
  text-transform: uppercase;
  font-weight: bold;
}

.line {
  width: 150px;
  height: 5px;
  background-color: white;
  clip-path: polygon(0 0, 100% 0, 95% 100%, 5% 100%);
}

/* Stats */
.stats {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  padding: 0px 50px;
  bottom: 250px;
}

.hd_stats {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-end;
}

.large_number {
  font-size: 50px;
}


@media only screen and (max-width: 1400px) {
  .stats {
    bottom: 100px;
  }
}

@media only screen and (max-width: 1200px) {
  #app {
    height: 100vh;
  }

  h1 {
    font-size: 50px;
  }

  h4 {
    font-size: 20px;
  }

  .large_number {
    font-size: 40px;
  }

  .stats {
    bottom: 45%;
    transform: translateY(50%);
  }

  .title {
    font-size: 50px;
  }

  .title span {
    font-size: 40px;
  }

  .kills {
    flex-direction: column;
    font-size: 100px;
  }

  .pcspecs {
    position: relative;
    bottom: 150px;
  }
}

@media only screen and (max-width: 800px) {
  #app {
    background-image: url("./assets/smallbg.png");
  }

  h1 {
    font-size: 30px;
  }

  h4 {
    font-size: 15px;
  }

  .large_number {
    font-size: 25px;
  }

  .title {
    font-size: 30px;
  }

  .title span {
    font-size: 20px;
  }

  .kills {
    flex-direction: column;
    font-size: 60px;
    margin: 20px 0;
  }

  .pcspecs {
    font-size: 10px;
    bottom: auto;
  }

  .specs {
    justify-content: center;
    width: auto;
  }
}

@media only screen and (max-width: 600px) {
  .stats {
    bottom: auto;
    -webkit-transform: translateY(0);
    transform: translateY(0);
    position: relative;
    display: auto;
  }

  .pcspecs {
    margin-top: 50px;
    margin-bottom: 25px;
  }
}

@media only screen and (max-height: 700px) {
  #app {
    height: 100%;
  }
}
</style>
