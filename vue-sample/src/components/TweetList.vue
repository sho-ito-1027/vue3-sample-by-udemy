<script setup lang="ts">
import { defineEmits } from 'vue';

type Tweet = {
    id: number,
    description: string,
}

type Props = {
    tweets: Tweet[]
}

const emit = defineEmits(['delete-tweet'])

const deleteTweet = (id: number) => {
    emit('delete-tweet', id)
}

defineProps<Props>()
</script>

<template>
    <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
        <span>{{ tweet.description }}</span>
        <button class="delete-button" @click="deleteTweet(tweet.id)">delete</button>
    </li>
</template>

<style scoped>
.tweet-list {
    list-style: none;
    margin-bottom: 12px;
    border-radius: 4px;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
    background-color: rgb(200, 222, 241);
    padding: 8px 20px;
    width: 300px;
}

.delete-button {
    color: #fff;
    font-weight: bold;
    background-color: #E2B651;
    border-radius: 2px;
    border: none;
    width: 60px;
    height: 22px;
}

.delete-button:hover {
    background-color: #BD7C37;
}
</style>