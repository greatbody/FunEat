<script setup lang="ts">
import { ref, onMounted, onBeforeMount } from 'vue'
const count = ref(0)
const message = ref("~~猜猜吃点啥~~");
const randomInt = (min: number, max: number) => Math.round(Math.random() * (max - min)) + min;
const foods = ["沙县小吃", "鱼粉", "洪湖小碗菜", "华莱士", "麦当劳", "肯德基"]
const previousFoodIndex = ref(-1)
const greet = (event: MouseEvent) => {
    if (previousFoodIndex.value === -1) {
        // If first time, set a random food
        previousFoodIndex.value = randomInt(0, foods.length - 1);
    } else {
        // Otherwise, set the next food but not the same with the previous one
        previousFoodIndex.value = findDifferentNumberWithinRange(0, foods.length - 1, previousFoodIndex.value);
    }
    message.value = foods[previousFoodIndex.value];
}

const findDifferentNumberWithinRange = (min: number, max: number, previousNumber: number): number => {
    let randomNumber = randomInt(min, max);
    while (randomNumber === previousNumber) {
        randomNumber = randomInt(min, max);
    }
    return randomNumber;
}

onMounted(() => {
    // alert('Message from mounted');
})

onBeforeMount(() => {
    // alert('Message from beforeMount');
})
</script>

<template>
    <div class="eat-what">今天吃点啥</div>
    <div class="bluebutton">
        <button class="btn-rollup" @click="greet">摇一摇</button>
    </div>
    <div class="food-name">{{ message }}</div>
</template>

<style>
.eat-what {
    font-size: 40px;
    font-weight: bold;
    color: #2c3e50;
    margin-top: 60px;
}

.showarea {
    width: 50%;
    height: 100px;
    border: 1px solid #ccc;
    padding: 10px;
}

.bluebutton {
    margin-top: 20px;
    margin: 5px;
    padding: 20px;
}

.btn-rollup {
    background-color: #3498db;
    color: #fff;
    border: none;
    padding: 10px 20px;
    font-size: 20px;
    cursor: pointer;
}

.food-name {
    font-size: 10em;
    font-weight: bold;
    color: #ff0000;
}
</style>