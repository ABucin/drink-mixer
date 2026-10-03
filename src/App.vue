<script setup lang="ts">
import {defineModel, onMounted, ref} from "vue";

const title = ref('Drink Mixer');
const drinks = ref([]);
const error = ref('');
const drinkModel = defineModel();

onMounted(() => {
      getDrinks();
    }
);

async function getDrinks() {
  try {
    const response = await fetch("http://localhost:8080/drinks");

    if (!response.ok) {
      throw new Error(await response.json());
    }

    drinks.value = await response.json();
  } catch (error) {
    error.value = error.name;
  }
}

async function addDrink() {
  const drink = {
    name: drinkModel.value,
  };

  try {
    const response = await fetch("http://localhost:8080/drinks", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(drink),
    });

    if (!response.ok) {
      const error = await response.json();
      throw new Error(error.name);
    }
  } catch (err: Error) {
    error.value = err;
  }
}

</script>

<template>
  <h1>{{ title }}</h1>

  <h2>Available drinks</h2>
  <ul>
    <li v-for="drink in drinks">{{ drink.name }}</li>
  </ul>
  <p>
    What cocktails you can make with current booze (+qty)
    1. provide alcohol + other (juice, syrup, water) + quantity
    2. app suggests recipes and highlights overlap (green for valid ingredients, grey/red for missing ones, orange for
    ones that exist but are insufficient)
    3. can provide natural words (?) (e.g. a bottle, a pinch, a bit, a lot)
  </p>
  <input v-model="drinkModel"/>
  <button @click="addDrink">Add drink</button>
  <p class="error" v-if="error">
    {{ error }}
  </p>
</template>

<style scoped>

</style>
