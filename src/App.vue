<script setup>
import { reactive } from 'vue'

const form = reactive({
  name: '',
  items: [''],
  insureItems: true,
  startDate: '',
  limitOfIndemnity: '',
  excess: ''
})

const completePolicy = () => {
  console.log(form);
}
</script>

<template>
  <main>
    <form @submit.prevent="completePolicy()">
    <input v-model="form.name" placeholder="Name" />

    <button @click.prevent="form.insureItems = true">Yes</button>
    <button @click.prevent="form.insureItems = false">No</button>

    <div v-if="form.insureItems">
      <div v-for="(item, index) in form.items" :key="index">
        <input v-model="form.items[index]" :placeholder="`Item ${index + 1}`" />
        <button @click.prevent="form.items.splice(index, 1)">Remove</button>
      </div>
      <button @click.prevent="form.items.push('')">Add another</button>
    </div>

    <input type="date" v-model="form.startDate" />

    <select v-model="form.limitOfIndemnity">
      <option disabled value="">Please select</option>
      <option value="1000">£1000</option>
      <option value="5000">£5000</option>
      <option value="10000">£10000</option>
    </select>


    <label><input type="radio" v-model="form.excess" value="250" /> £250</label>
    <label><input type="radio" v-model="form.excess" value="500" /> £500</label>
    <label><input type="radio" v-model="form.excess" value="1000" /> £1000</label>

    <button type="submit">Submit</button>
    </form>
  </main>
</template>
