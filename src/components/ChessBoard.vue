<template>
    <div class="chess-board">
        <div v-for="(row, rowIndex) in board" :key="rowIndex" class="chess-row">
            <div v-for="(col, colIndex) in row" :key="colIndex" class="chess-col">
                <div :class="['box', selected]" @click="selectPiece(rowIndex, colIndex)" @mousedown="abc()">
                    <ChessPiece v-if="col" :class="col.color" :type="col.type" :color="col.color" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ChessPiece from './ChessPiece.vue';

export default {
    components: {
        ChessPiece,
    },
    data() {
        return {
            size: 8,
            pieces: {
                pawn: 'pawn',
                rook: 'rook',
                knight: 'knight',
                bishop: 'bishop',
                queen: 'queen',
                king: 'king'
            },
            colors: {
                white: 'white',
                black: 'black'
            },
            board: [
                [{ type: 'rook', color: 'black' }, { type: 'knight', color: 'black' }, { type: 'bishop', color: 'black' }, { type: 'queen', color: 'black' }, { type: 'king', color: 'black' }, { type: 'bishop', color: 'black' }, { type: 'knight', color: 'black' }, { type: 'rook', color: 'black' }],
                [{ type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }, { type: 'pawn', color: 'black' }],
                [null, null, null, null, null, null, null, null],
                [null, null, null, null, null, null, null, null],
                [null, null, null, null, null, null, null, null],
                [null, null, null, null, null, null, null, null],
                [{ type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }, { type: 'pawn', color: 'white' }],
                [{ type: 'rook', color: 'white' }, { type: 'knight', color: 'white' }, { type: 'bishop', color: 'white' }, { type: 'queen', color: 'white' }, { type: 'king', color: 'white' }, { type: 'bishop', color: 'white' }, { type: 'knight', color: 'white' }, { type: 'rook', color: 'white' }]
            ],
            temp: [],
            selected: null,
            selectedSquare: null,
        };
    },
    created() {
        for (let row = 0; row < this.size; row++) {
            this.temp[row] = [];
            for (let col = 0; col < this.size; col++) {
                let piece = this.temp[row][col];
                if (piece) {
                    this.temp.push({
                        // row,
                        // col,
                        type: piece.type,
                        color: piece.color
                    });
                }
            }
        }
    },
    methods: {
        selectPiece(row, col) {
            console.log(this.board[row][col]);
        },
        // ???????????????????????????????????????????????????????????????????????????
        canMoveTo(row, col) {
            // ???????????????????????????????????????
            if (row < 0 || col < 0 || row >= this.size || col >= this.size) {
                return false
            }
            // ??????????????????????????????????????????
            const pieceAtDestination = this.pieces.find(p => p.row === row && p.col === col)
            if (pieceAtDestination) {
                return false
            }
            return true
        },
        abc() {
            console.log(this);
        }
    }
};
</script>
<style scoped>
.selected {
    background-color: #e0872f98;
}

/* ????????????????????? */
.chess-board {
    display: flex;
    flex-wrap: wrap;
    width: 800px;
    /* ?????????????????? */
    height: 800px;
    margin: auto;
    border: 1rem solid rgb(239, 183, 160);
    /* ?????????????????? */
    /* background-color: #e0872f98; */
}

/* ???????????? */
.chess-row {
    display: flex;
    width: 100%;
}

/* ???????????? */
.chess-col {
    box-sizing: border-box;
    width: 12.5%;
    height: 0;
    padding-bottom: 12.5%;
    position: relative;
}

/* ???????????? */
.box {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.chess-row:nth-of-type(odd) .chess-col:nth-child(odd) {
    background-color: rgb(210, 154, 129);
}

.chess-row:nth-of-type(odd) .chess-col:nth-child(even) {
    background-color: rgb(152, 123, 103);
}

.chess-row:nth-of-type(even) .chess-col:nth-child(odd) {
    background-color: rgb(152, 123, 103);
}

.chess-row:nth-of-type(even) .chess-col:nth-child(even) {
    background-color: rgb(210, 154, 129);
}

/* ?????? */
@media (max-width: 800px) {
    .chess-board {
        width: 600px;
        height: 600px;
    }
}

@media (max-width: 600px) {
    .chess-board {
        width: 400px;
        height: 400px;
    }
}
</style>
