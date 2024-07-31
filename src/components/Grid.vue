<script setup>
import { ref } from 'vue'
const Elements = ref([' ',' ',' ',' ',' ',' ',' ',' ',' ']);
const player = ref('X');

function play(n) {
    if (this.player === 'X' && !['X','O'].includes(this.Elements[n])) {
        this.Elements[n] = 'X';
        this.player = 'O';
    }
    else if (this.player === 'O' && !['X','O'].includes(this.Elements[n])) {
        this.Elements[n] = 'O';
        this.player = 'X';
    }
}

function reset() {
    this.Elements = [' ',' ',' ',' ',' ',' ',' ',' ',' ']
}

</script>
<template>
    <div class="grid text-center" style="margin: 50px auto; max-width: 400px;">
        <div class="row no-gutters">
            <div class="case col-4 p-3" v-for="n in [0,1,2,3,4,5,6,7,8]" style="border: 0.1rem solid; height: 8rem;" @click="play(n)">
                {{ Elements[n] }}
            </div>
        </div>
    </div>
    <div class="text-center" style="font-weight: bold;">
        Au tour de : {{ player }}
    </div>
    <div class="text-center mt-4">
        <button class="btn btn-secondary" style="border: 1rem; font-weight: bold;" @click="reset()">RESET</button>
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
</style>