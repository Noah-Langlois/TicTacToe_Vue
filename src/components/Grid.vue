<script setup>
import { ref } from 'vue'
const Elements = ref([' ',' ',' ',' ',' ',' ',' ',' ',' ']);
const player = ref('X');
const isWon = ref(false);

function checkWin() {
    for (const i of [0,3,6]) {
        if (this.Elements[i] === this.Elements[i+1] && this.Elements[i+1] === this.Elements[i+2] && this.Elements[i] != ' ') {
            this.isWon = true;
        }
    }
    for (const i of [0,1,2]) {
        if (this.Elements[i] === this.Elements[i+3] && this.Elements[i+3] === this.Elements[i+6] && this.Elements[i] != ' ') {
            this.isWon = true;
        }
    }
    if (this.Elements[0] === this.Elements[4] && this.Elements[4] === this.Elements[8] && this.Elements[0] != ' ') {
        this.isWon = true;
    }
    if (this.Elements[6] === this.Elements[4] && this.Elements[4] === this.Elements[2] && this.Elements[6] != ' ') {
        this.isWon = true;
    }
}

function play(n) {
    if (this.isWon === false) {
        if (this.player === 'X' && !['X','O'].includes(this.Elements[n])) {
            this.Elements[n] = 'X';
            this.checkWin();
            if (this.isWon === false) {
                this.player = 'O';
            }
        }
        else if (this.player === 'O' && !['X','O'].includes(this.Elements[n])) {
            this.Elements[n] = 'O';
            this.checkWin();
            if (this.isWon === false) {
                this.player = 'X';
            }
        }
    }
}

function reset() {
    this.Elements = [' ',' ',' ',' ',' ',' ',' ',' ',' ']
    this.isWon = false
}

</script>
<template>
    <div class="grid text-center" style="margin: 50px auto; max-width: 400px;">
        <div class="row no-gutters">
            <div class="case col-4 p-3" v-for="n in [0,1,2,3,4,5,6,7,8]" style="height: 8rem;" @click="play(n)"
            :class="{'border_top' : [0,1,2].includes(n), 'border_bottom' : [6,7,8].includes(n), 'border_left' : [0,3,6].includes(n), 'border_right' : [2,5,8].includes(n)}"
            >
                {{ Elements[n] }}
            </div>
        </div>
    </div>
    <div class="text-center" style="font-weight: bold;" v-if="!isWon">
        Au tour de : {{ player }}
    </div>
    <div class="text-center" style="font-weight: bold;" v-if="isWon">
        {{ player }} a gagné !
    </div>
    <div class="text-center mt-4">
        <button class="btn btn-primary" style="border: 1rem; font-weight: bold;" @click="reset()">RESET</button>
    </div>
</template>
<style scoped>
    .case {
        font-weight: bold;
        font-size: 2rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    .border_top {
        border-bottom: 0.1rem solid;
    }
    .border_bottom {
        border-top: 0.1rem solid;
    }
    .border_left {
        border-right: 0.1rem solid;
    }
    .border_right {
        border-left : 0.1rem solid;

    }
</style>