<script setup lang="ts">
import { ref, toRefs } from '@vue/reactivity';
import { onBeforeMount, onMounted, onUpdated, reactive, watch } from 'vue';

const item1 = reactive({
    name: 'Desk',
    price: 40000,
})

const item2 = reactive({
    name: 'Bike',
    price: 20000,
})

const url1 = 'https://www.amazon.co.jp/dp/B09QMBH5R7'

const buy = (itemName: string) => {
    alert('Are you sure to buy ' + itemName + ' ?')
}

const clear = () => {
    item1.name = ''
    item1.price = 0
}

const message: string = ''

const budget: number = 50000

const priceLabel = ref<string>(item1.price + ' yen')
const { price } = toRefs(item1)
watch(price, () => {
    if (price.value > budget * 2) {
        priceLabel.value = 'tooooooo expensive..'
        return
    }
    if (price.value > budget) {
        priceLabel.value = 'expensive..'
        return
    }
    priceLabel.value = price.value + ' yen'
})

onBeforeMount(() => {
    console.log('on before mounted')
})

onMounted(() => {
    console.log('on mounted')
})

onUpdated(() => {
    console.log('on updated')
})

</script>

<template>
    <div class="container">
        <h1>Payment</h1>
        <input v-model="item1.name" />
        <input v-model="item1.price" />
        <button v-on:click="clear">Clear</button>
        <div class="payment">
            <label>{{ item1.name }}</label>
            <label>{{ priceLabel }}</label>
            <a v-bind:href="url1">bought at ...</a>
            <button v-on:click="buy(item1.name)">BUY</button>
        </div>
        <div class="payment">
            <label>{{ item2.name }}</label>
            <label>{{ item2.price + ' yen' }}</label>
            <button v-on:click="buy(item1.name)">BUY</button>
        </div>
    </div>
</template>

<style scoped>
label {
    font-size: 20px;
    font-weight: bold;
}

input {
    margin-bottom: 8px;
}
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.payment {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    width: 400px;
    background-color: aliceblue;
    margin-bottom: 8px;
}
</style>