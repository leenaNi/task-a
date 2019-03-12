<template>
  <div id="app">
    <h2>Tik Tac Toe</h2>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <div class="grid-container">
            <div class="grid-item" v-for="t in tikTac" :key="'s'+t">{{t}}</div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label class="control-label">Player {{player}} enter number:</label>
                <input class="form-control" v-model.number="playerInput" v-on:keyup.13="draw" />
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
  name: "app",
  data() {
    return {
      tikTac: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      player: 1,
      playerInput: ''
    };
  },
  methods: {
    draw(){
      console.log(this.playerInput);      
      this.tikTac[(this.playerInput-1)] = (this.player===1)? 'X': 'O';
      this.playerInput = '';
      this.player = 2;
    },
    checkWinner(){

    }
  }
};
</script>
<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";
</style>
<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.grid-container {
  display: grid;
  grid-row-gap: 50px;
  grid-template-columns: auto auto auto;
  background-color: #2196f3;
  padding: 10px;
}

.grid-item {
  background-color: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  padding: 20px;
  font-size: 30px;
  text-align: center;
}
</style>
