<script setup>
  import { getPotions,createPotions } from "../api/potions";
</script>

<script>
  export default {
    name: "PotionManager",
    data() {
      return {
        potions: [],

        newPotion: {
          name: "",
          effect: "",
          isDangerous: false,
        },
      };
    },
    methods: {
      async loadPotions() {
        this.potions = await getPotions();
      },
      async submitCreatedPotion() {
        await createPotion(this.newPotion);
      },
    },
    mounted() {
      this.loadPotions();
    },
  };
</script>

<template>
  <form @submit.prevent="createPotions" class="">
    <label for="name" class="">Name</label>
    <input
      v-model="newPotion.name"
      type="text"
      name="name"
      id=""
      class="border-bs-gray-950 border-solid"
    />

    <label for="effect" class="">Effect</label>
    <input
      v-model="newPotion.effect"
      type="text"
      name="effect"
      id=""
      class="border-bs-gray-950 border-solid"
    />

    <label for="dangerous" class="">Is Dangerous</label>
    <input
      v-model="newPotion.isDangerous"
      type="checkbox"
      name="dangerous"
      id=""
      class="border-bs-gray-950 border-solid"
    />

    <button class="border-solid border-2" type="submit" >Létrehozás</button>
  </form>

  <table class="">
    <thead class="">
      <tr class="">
        <td>Id</td>
        <td>Name</td>
        <td>Effect</td>
        <td>isDangerous</td>
        <td>Action</td>
      </tr>
    </thead>
    <tbody class="">
      <tr v-for="potion in potions" :key="potion.id">
        <td>{{ potion.id }}</td>
        <td>{{ potion.name }}</td>
        <td>{{ potion.effect }}</td>
        <td>{{ potion.isDangerous ? "Yes" : "No" }}</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</template>
