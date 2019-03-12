<template>
  <div id="app">
    <h2>Tik Tac Toe</h2>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <table class="table" id="tictactoe">
            <tr v-for="tr in 3" :key="'tr'+tr">
              <td height="120" width="120" align="center" valign="center" v-for="td in 3"
               :key="'td'+td" @click="draw($event)" :class="(td==tr)? ('diagonal0 row'+tr+' col'+td) : (td== (3-tr)-1)? (' diagonal1 row'+tr+' col'+td): ('row'+tr+' col'+td) "></td>
            </tr>
          </table>
        </div>
        <div class="col-md-6">
          <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label class="control-label">Player {{turn}} turn</label><br/>
               <button class="btn btn-sm btn-primary" @click="startNewGame" v-if="scores['X']>0|| scores['O']>0">Reset</button>
              </div>
              <br/>
              <span v-if="scores['X']>0|| scores['O']>0">
                <label class="alert alert-info">Player X win {{scores['X']}} times</label><br/>
                <label class="alert alert-info">Player O win {{scores['O']}} times</label>
              </span>
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
      moves: 0,
      turn: 'X',
      scores: {'X': 0, 'O': 0}
    };
  },
  methods: {
    draw(e){
      if (e.target.innerHTML !== '') {
        return;
      }
      e.target.innerHTML = this.turn;
      this.moves += 1;
      if (this.win(e.target.className)) {
        this.scores[this.turn] = this.scores[this.turn]+1;
          alert('Winner: Player ' + this.turn);
          this.startNewGame();
      } else if (this.moves === 9) {
          alert("Draw");
          this.startNewGame();
      } else {
          this.turn = (this.turn === "X") ? "O" : "X";
      }
    },
    startNewGame() {
      this.moves = 0;
      this.turn = "X";
      var table = document.getElementById("tictactoe");
      for (var i = 0, row; row = table.rows[i]; i++) {
        for (var j = 0, col; col = row.cells[j]; j++) {
          col.innerHTML = '';
        }
      }
    },
    win(clickedClass) {
      // Get all cell classes
      var memberOf = clickedClass.split(/\s+/);
      for (var i = 0; i < memberOf.length; i++) {
          var testClass = '.' + memberOf[i];
          var items = this.contains('#tictactoe ' + testClass, this.turn);
          // winning condition: turn == 3
          if (items.length == 3) {
              return true;
          }
      }
      return false;
    },
    contains(selector, text) {
      var elements = document.querySelectorAll(selector);
      return [].filter.call(elements, function (element) {
          return RegExp(text).test(element.textContent);
      });
    }
  },
  created() {
  },
};
</script>
<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";

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
  grid-row-gap: 10px;
  grid-template-columns: auto auto auto;
  background-color: #ffffff;
  padding: 10px;
}

.grid-item {
  background-color: black;
  border: 3px solid white;
  padding: 10px;
  font-size: 30px;
  text-align: center;
}
    table {
	border-collapse:collapse;
}

td {
	background-color: black;
	border: 3px solid white;
	font-size:80px;
	color:#ffffff;
	border-radius: 10px 10px 10px 10px;
}
</style>
