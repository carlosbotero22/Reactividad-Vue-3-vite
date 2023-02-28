<template>
  <h1>{{ title }}</h1>
  <h2 :class="classCounter">{{ counter }}</h2>
  <button @click="increment">aumentar</button>
  <button @click="decrement">disminuir</button>
  <button @click="reset">reset</button>
  <button @click="add" :disabled="bloquearBtnAdd">Add</button>

  <br />
  <ul v-for="(num, index) in arrayNumbers" :key="index">
    <li>{{ num }}</li>
  </ul>
</template>

<!-- ************************************************* -->

<script setup>
import { ref, computed } from 'vue';

const title = 'Vite + Vue';

const counter = ref(0);

const increment = () => counter.value++;
const decrement = () => counter.value--;
const reset = () => (counter.value = 0);

const arrayNumbers = ref([]);

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero';
  }

  if (counter.value > 0) {
    return 'positive';
  }

  if (counter.value < 0) {
    return 'negative';
  }
});

const add = () => {
  arrayNumbers.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayNumbers.value.find((num) => num === counter.value);
  return numSearch || numSearch === 0;
});
</script>

<!-- ************************************************* -->

<style scoped>
.read-the-docs {
  color: #888;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: gray;
}
</style>
