<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from 'vue';

const inputtingName = ref<string>('')
const inputtingAge = ref<number>(0)

const emit = defineEmits([
  'register'
])

const register = () => {
  const person = { id: Math.random(), name: inputtingName.value, age: inputtingAge.value }
  emit('register', person)
  inputtingName.value = ''
  inputtingAge.value = 0
}

const nameLengthLimit = 15

const isValidName = computed(() => {
  if (inputtingName.value.length >= nameLengthLimit) {
    return false
  }
  return true
})

const color = computed(() => {
  return isValidName.value ? 'white' : 'rgb(244,194,190)'
})

</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-column">
        <span>name:</span>
        <input class="input-name" v-model="inputtingName" />
      </div>
      <soan class="error-message" v-if="!isValidName"> {{nameLengthLimit}} characters or less, please.</soan>
      <div class="input-column">
        <span>age:</span>
        <input class="input" v-model="inputtingAge" type="number" />
      </div>
    </div>
    <button :disabled="!isValidName" class="register-button" @click="register">register</button>
  </div>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(255, 241, 226);
  padding: 24px 0;
  width: 50%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.input-name {
  background-color: v-bind(color);
}
.input-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 50%;
  margin-bottom: 20px;
}

.input-column {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

input {
  width: 120px;
  margin-bottom: 8px;
}

span {
  font-size: 20px;
  font-weight: bold;
}
.error-message {
  font-size: 12px;
  color: rgb(244, 194, 190);
}
</style>
