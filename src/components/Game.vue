<template>
  <div style="flex:1">
       <div style="position:relative">
             <div v-if="winner" class="state">You win </div>
             <div v-if="loser" class="state">You lost </div>
     
    <canvas width="400" height="400">

    </canvas>
       </div>
    <!-- <div class="controls-wrapper">
      <ul id="events"></ul>
      <div class="controls">
        <div class="chat-wrapper">
          <form id="chat-form">
            <input id="chat" autocomplete="off" title="chat" />
            <button id="say">Say</button>
          </form>
        </div>
      </div>
    </div> -->
  </div>
</template>

<script>
export default {
    data() {
        return {
            winner:false,
            loser:false,
        }
    },
  methods: {
    getClickCoordinates( event) {
    const canvas = document.querySelector("canvas");

      const { top, left } = canvas.getBoundingClientRect();
      const { clientX, clientY } = event;
      return {
        x: clientX - left,
        y: clientY - top,
      };
    },
    log: (text) => {
      const parent = document.querySelector("#events");
      const el = document.createElement("li");
      el.innerHTML = text;

      parent.appendChild(el);
      parent.scrollTop = parent.scrollHeight;
    },

    onChatSubmitted: (sock) => (e) => {
      e.preventDefault();

      const input = document.querySelector("#chat");
      const text = input.value;
      input.value = "";

      sock.emit("message", text);
    },

    createBoard: ( numCells = 10) => {
    const canvas = document.querySelector("canvas");

      const ctx = canvas.getContext("2d");

      const cellSize = Math.floor(400 / numCells);
      
      const fillCell = (x, y, color) => {
        ctx.shadowOffsetX = 0;
ctx.shadowOffsetY = 0;
ctx.shadowBlur    = 0;
ctx.shadowColor   = "";
        ctx.fillStyle = color;
        ctx.fillRect(x * cellSize+4, y * cellSize+4, cellSize-7, cellSize-7);
      };

      const clear = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
         ctx.fillStyle = '#374bb713';

      ctx.fillRect(0,0,400,400)
      };

      const drawGrid = () => {
ctx.shadowOffsetX = 1;
ctx.shadowOffsetY = 3;
ctx.shadowBlur    = 5;
ctx.shadowColor   = "gray";
        ctx.beginPath();


        ctx.lineJoin = "round"
        for (let i = 0; i < numCells + 1; i++) {
          ctx.moveTo(i * cellSize, 0);
          ctx.lineTo(i * cellSize, (numCells) * cellSize);
          ctx.moveTo(0, i * cellSize);
          ctx.lineTo(numCells * cellSize, i * cellSize);
            ctx.lineWidth = 7;
          
        }
var gradient = ctx.createLinearGradient(0, 0, numCells * cellSize, 0);
gradient.addColorStop("0", "magenta");
gradient.addColorStop("0.5" ,"#FFDB00");
gradient.addColorStop("1.0", "red");
        ctx.strokeStyle='#374bb7';
        ctx.stroke();
      };

      const drawBoard = (board) => {
        board.forEach((row, y) => {
          row.forEach((color, x) => {
            color && fillCell(x, y, color);
          });
        });
      };

      const reset = (board = []) => {
        clear();
        drawGrid();
        drawBoard(board);
      };

      const getCellCoordinates = (x, y) => ({
        x: Math.floor(x / cellSize),
        y: Math.floor(y / cellSize),
      });

      return { fillCell, reset, getCellCoordinates };
    },
  },
  sockets:{
      win() {
     this.winner = true
     this.loser = false
    },
      loose() {
     this.winner = false
     this.loser = true
    },
message() {
    //   this.log(text)
    },
    turn({ x, y, color }) {
    const { fillCell } = this.createBoard();

        fillCell(x, y, color)
    },
      board(board) {
    const {  reset } = this.createBoard();

        reset(board)
        setTimeout(() => {
             this.winner = false
     this.loser = false
        }, 6000);
    }
  },
  mounted() {
     const canvas = document.querySelector("canvas");
    const { fillCell, reset, getCellCoordinates } = this.createBoard();

    const onClick = (e) => {
      const { x, y } = this.getClickCoordinates( e);
      this.$socket.emit("turn", getCellCoordinates(x, y));
    };

    // this.$socket.on("message", this.log);
    // this.$socket.on("turn", ({ x, y, color }) => fillCell(x, y, color));
    // this.$socket.on("board", reset);

    // document
    //   .querySelector("#chat-form")
    //   .addEventListener("submit", this.onChatSubmitted(this.$socket));

    canvas.addEventListener("click", onClick);
  },
};
</script>

<style>
.state{
    width: 400px;
        font-weight: bold;
    height: 400px;
    position: absolute;
    /* margin: 10px auto; */
    background: #0500006b;
    color: #fff;
    left: 50%;
    z-index: 555;
    transform: translateX(-50%);
    font-size: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>