<template>
  <div>
    <h1
      class="text-black mt-[40px] text-6xl font-semibold text-center font-ubuntu"
    >
      Who will be win?
    </h1>
  </div>
  <div>
    <h1 class="text-black mt-5 text-5xl font-medium text-center font-ubuntu">
      <span v-if="!X_win && !O_win && !Draw"> {{ player }} Turn</span>
      <span v-if="X_win">X win</span>
      <span v-if="O_win">O win</span>
      <span v-if="Draw">Draw</span>
    </h1>
  </div>
  <div class="flex justify-center items-center">
    <h1
      v-if="X_win || O_win || Draw"
      class="py-2 px-4 mt-5 mb-3 font-medium text-xl font-ubuntu bg-gray-400 hover:bg-slate-300"
    >
      <button @click="resetGame(N)">play Again</button>
    </h1>
  </div>
  <div
    v-if="!X_win && !O_win && !Draw"
    class="flex justify-center items-center my-5"
  >
    <button
      @click="N--"
      class="text-black px-3 font-medium text-3xl font-ubuntu"
      v-if="N >= 4"
    >
      -
    </button>
    <h1 class="text-black px-3 font-medium text-3xl font-ubuntu bg-gray-400">
      {{ N }}
    </h1>
    <button
      @click="N++"
      class="text-black px-3 font-medium text-3xl font-ubuntu"
    >
      +
    </button>
  </div><div class="flex justify-center items-center">
  <div 
    class="grid gap-1 w-96 "
    :style="{ 'grid-template-columns': `repeat(${N}, minmax(0, 1fr))` }"
  >
    <button
      v-for="(cell, index) in values"
      :key="index"
      class="bg-gray-400 p-4 flex justify-center items-center aspect-square hover:bg-slate-300 text-black px-3 font-normal text-5xl font-ubuntu"
      @click="play(index)"
      :disabled="cell !== null || X_win || O_win || Draw"
    >
      {{ cell === "X" ? "X" : cell === "O" ? "O" : "" }}
    </button>
  </div></div>

  <div>
    <div class="w-full border-t-2 border-gray-300 mt-[50px] mb-[20px]"></div>
    <h1
      class="items-center text-3xl font-semibold text-center font-ubuntu mt-[-40px]"
    >
      History
    </h1>
    <div v-if="this.history.length > 0">
      <div class="grid grid-cols-2 gap-5 mx-10 my-10">
        <div>
          <div class=" grid-cols-2 gap-5  my-10">
            <div
              v-for="(history, index) in history"
              :key="index"
              class="flex justify-start items-start"
            >
              <button
                @click="showHistory(index)"
                class="rounded-lg py-2 px-4 mt-3 font-medium text-xl font-ubuntu bg-gray-400 hover:bg-slate-300"
              >
                Game : {{ index + 1 }}
              </button>
            </div>
          </div>
          <div class="flex justify-start">
            <button @click="clearHistory" class="text-xl font-normal font-ubuntu">
              clearHistory
            </button>
          </div>

        </div>
        <div>
          <div v-for="(selcet_, index) in selcet_H" :key="index">
            <h1
              class="flex justify-center items-center my-3 text-black px-3 font-semibold text-2xl font-ubuntu"
            >
              {{ selcet_.win }}
            </h1>
            <div class="flex justify-center items-center">
              <div
                class="grid gap-1 w-50 "
                :style="{
                  'grid-template-columns': `repeat(${selcet_.size}, minmax(0, 1fr))`,
                }"
              >
                <div
                  v-for="(cell, index) in selcet_.value"
                  :key="index"
                  class="bg-gray-300 p-4 flex justify-center items-center aspect-square text-black px-3 font-semibold text-xs font-ubuntu"
                >
                  {{ cell }}
                </div>
              </div>
            </div>
    
            <h1
              class="flex justify-center items-center my-3 text-black px-3 font-semibold text-2xl font-ubuntu"
            >
              select box order: {{ selcet_.order }}
            </h1>
          </div>

        </div>
      </div>


      </div> 
      
    <div
      v-else
      class="text-3xl font-semibold text-center font-ubuntu text-gray-400 mt-[40px]"
    >
      No history
    </div>
  </div>
</template>

<script>
export default {
  name: "TicTacToe",
  data() {
    return {
      N: 3,
      player: "X",
      X_win: false,
      O_win: false,
      Draw: false,
      row_O: [],
      col_O: [],
      row_X: [],
      col_X: [],
      cross_O: 0,
      xcross_O: 0,
      cross_X: 0,
      xcross_X: 0,
      values: [],
      order: [],
      history: [],
      selcet_H: [],
      result: "",
    };
  },
  methods: {
    play(index) {
      this.order.push(index + 1);
      console.log(this.order);
      if (
        this.values[index] === null &&
        !this.X_win &&
        !this.O_win &&
        !this.Draw
      ) {
        this.values[index] = this.player;
        console.log("Values:", this.values);
        this.checkWin(index);
        if (!this.X_win && !this.O_win && !this.Draw) {
          this.player = this.player === "X" ? "O" : "X";
        }
      }
    },
    checkWin(index) {
      const adjustIndex = index + 1;
      let row = 0;
      let col = 0;
      if (this.player === "X" && !this.O_win) {
        if (adjustIndex % this.N === 0) {
          row = Math.floor(adjustIndex / this.N);
        } else {
          row = Math.floor(adjustIndex / this.N) + 1;
        }
        this.row_X.push(row);
        if (adjustIndex % this.N === 0) {
          col = this.N;
        } else {
          col = adjustIndex % this.N;
        }
        this.col_X.push(col);
        if (row === col) {
          this.cross_X += 1;
          if (this.cross_X === this.N) {
            this.X_win = true;
          }
        }
        if (row + col === this.N + 1) {
          this.xcross_X += 1;
          if (this.xcross_X === this.N) {
            this.X_win = true;
          }
        }
        let count_col = this.col_X.reduce((acc, num) => {
          acc[num] = (acc[num] || 0) + 1;
          return acc;
        }, {});
        let count_row = this.row_X.reduce((acc, num) => {
          acc[num] = (acc[num] || 0) + 1;
          return acc;
        }, {});
        if (
          Object.values(count_col).some((value) => value === this.N) ||
          Object.values(count_row).some((value) => value === this.N)
        ) {
          this.X_win = true;
        }
        row = 0;
        col = 0;
      }
      if (this.player === "O" && !this.X_win) {
        if (adjustIndex % this.N === 0) {
          row = Math.floor(adjustIndex / this.N);
        } else {
          row = Math.floor(adjustIndex / this.N) + 1;
        }
        this.row_O.push(row);
        if (adjustIndex % this.N === 0) {
          col = this.N;
        } else {
          col = adjustIndex % this.N;
        }
        this.col_O.push(col);
        if (row === col) {
          this.cross_O += 1;
          if (this.cross_O === this.N) {
            this.O_win = true;
          }
        }
        if (row + col === this.N + 1) {
          this.xcross_O += 1;
          if (this.xcross_O === this.N) {
            this.O_win = true;
          }
        }
        let count_col = this.col_O.reduce((acc, num) => {
          acc[num] = (acc[num] || 0) + 1;
          return acc;
        }, {});
        let count_row = this.row_O.reduce((acc, num) => {
          acc[num] = (acc[num] || 0) + 1;
          return acc;
        }, {});
        if (
          Object.values(count_col).some((value) => value === this.N) ||
          Object.values(count_row).some((value) => value === this.N)
        ) {
          this.O_win = true;
        }
        row = 0;
        col = 0;
      }
      if (!this.X_win && !this.O_win && !this.values.includes(null)) {
        this.Draw = true;
      }
      if (this.X_win || this.O_win || this.Draw) {
        let who_W;
        if (this.X_win) {
          who_W = "X win";
        } else if (this.O_win) {
          who_W = "O win";
        } else if (this.Draw) {
          who_W = "Draw";
        }
        this.history.push({
          value: this.values,
          size: this.N,
          order: this.order,
          win: who_W,
        });
      }
    },
    resetGame(size) {
      this.N = size || this.N;
      this.player = "X";
      this.X_win = false;
      this.O_win = false;
      this.Draw = false;
      this.row_O = [];
      this.col_O = [];
      this.row_X = [];
      this.col_X = [];
      this.order = [];
      this.cross_O = 0;
      this.xcross_O = 0;
      this.cross_X = 0;
      this.xcross_X = 0;
      this.values = Array.from({ length: this.N * this.N }, () => null);
    },
    clearHistory() {
      this.history = [];
      this.selcet_H = []
    },
    showHistory(index) {
      this.selcet_H = [
        {
          value: this.history[index].value,
          size: this.history[index].size,
          order: this.history[index].order,
          win: this.history[index].win,
        },
      ];
    },
  },

  watch: {
    N(newN) {
      this.values = Array.from({ length: newN * newN }, () => null);
    },
  },
  created() {
    this.values = Array.from({ length: this.N * this.N }, () => null);
  },
};
</script>
