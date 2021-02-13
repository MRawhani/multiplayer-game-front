<template>
  <div>
    <canvas width="400" height="400"></canvas>
    <div class="controls-wrapper">
      <ul id="events"></ul>
      <div class="controls">
        <div class="chat-wrapper">
          <form id="chat-form">
            <input id="chat" autocomplete="off" title="chat" />
            <button id="say">Say</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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

    createBoard: ( numCells = 20) => {
    const canvas = document.querySelector("canvas");

      const ctx = canvas.getContext("2d");

      const cellSize = Math.floor(400 / numCells);

      const fillCell = (x, y, color) => {
        ctx.fillStyle = color;
        ctx.fillRect(x * cellSize+2, y * cellSize+2, cellSize-4, cellSize-4);
      };

      const clear = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      };

      const drawGrid = () => {
        ctx.beginPath();

        for (let i = 0; i < numCells + 1; i++) {
          ctx.moveTo(i * cellSize, 0);
          ctx.lineTo(i * cellSize, numCells * cellSize);

          ctx.moveTo(0, i * cellSize);
          ctx.lineTo(numCells * cellSize, i * cellSize);
           ctx.lineWidth = 4;
        }
var gradient = ctx.createLinearGradient(0, 0, numCells * cellSize, 0);
gradient.addColorStop("0", "magenta");
gradient.addColorStop("0.5" ,"blue");
gradient.addColorStop("1.0", "red");
        ctx.strokeStyle=gradient;
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
message(text) {
      this.log(text)
    },
    turn({ x, y, color }) {
    const { fillCell } = this.createBoard();

        fillCell(x, y, color)
    },
      board(board) {
    const {  reset } = this.createBoard();

        reset(board)
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

    document
      .querySelector("#chat-form")
      .addEventListener("submit", this.onChatSubmitted(this.$socket));

    canvas.addEventListener("click", onClick);
  },
};
</script>

<style>
</style>