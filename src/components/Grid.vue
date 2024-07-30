<script setup>
import { ref } from 'vue'
const Elements = [0,1,2,3,4,5,6,7,8];
</script>
<template>
    <div class="grid text-center" style="margin: 50px auto; max-width: 400px;">
        <div class="row no-gutters">
            <div class="case col-4" v-for="n in Elements">
                X
            </div>
        </div>
    </div>
</template>
<style>
</style>