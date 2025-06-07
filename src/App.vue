<script setup>
import { reactive } from 'vue'
import RadioButtons from './components/radio-buttons.vue';

const form = reactive({
  name: '',
  items: [''],
  insureItems: true,
  startDate: '',
  limitOfIndemnity: '',
  excess: ''
});

const excessOptions = [
  { value: '250', name: 'excess' },
  { value: '500', name: 'excess' },
  { value: '1000', name: 'excess' }
];

const insureItemsOptions = [
  { value: 'Yes', name: 'insureItems' },
  { value: 'No', name: 'insureItems' }
];

const today = new Date();
const minDate = today.toISOString().split('T')[0];

const futureDate = new Date();
futureDate.setDate(today.getDate() + 15);
const maxDate = futureDate.toISOString().split('T')[0];

const updateExcess = (value) => {
  form.excess = value;
}

const updateInsureItems = (value) => {
  form.insureItems = value === 'Yes' ? true : false;
  if (!form.insureItems) {
    form.items = [''];
  }
}

const completePolicy = () => {
  console.log(form);
}
</script>

<template>
  <main>
    <h1>Insurance Policy</h1>
    <form @submit.prevent="completePolicy()">
      <div>
        <h2>Customer</h2>
        <label for="name">Name</label>
        <input id="name" v-model="form.name" placeholder="Enter name" required />
      </div>

      <div>
        <h2>Items</h2>

      <RadioButtons :radioOptions="insureItemsOptions" legendText="Do you want to insure items?" @radio-updated="updateInsureItems" :checked="form.insureItems === true ? 'Yes' : 'No'" />

      <div v-if="form.insureItems">
        <fieldset>
          <legend>Items to Insure</legend>
          <div
            v-for="(item, index) in form.items"
            :key="index"
            :aria-label="`Item ${index + 1}`"
          >
            <label :for="`item-${index}`">Item {{ index + 1 }}</label>
            <input
              :id="`item-${index}`"
              v-model="form.items[index]"
              :placeholder="`Item ${index + 1}`"
            />
            <button
              v-if="form.items.length > 1"
              @click.prevent="form.items.splice(index, 1)"
              type="button"
              aria-label="Remove item"
            >
              Remove
            </button>
          </div>
          <button @click.prevent="form.items.push('')" type="button">
            Add another
          </button>
        </fieldset>
      </div>
      </div>

      <div>
        <h2>Policy</h2>
        <label for="startDate">Start Date</label>
        <input
          type="date"
          id="startDate"
          v-model="form.startDate"
          :min="minDate"
          :max="maxDate"
          required
        />
      </div>

      <div>
        <label for="limitOfIndemnity">Limit of Indemnity</label>
        <select id="limitOfIndemnity" v-model="form.limitOfIndemnity" required>
          <option disabled value="">Please select</option>
          <option value="1000000">£1,000,000</option>
          <option value="2000000">£2,000,000</option>
          <option value="5000000">£5,000,000</option>
        </select>
      </div>

      <RadioButtons :radioOptions="excessOptions" legendText="Excess" @radio-updated="updateExcess" :checked="form.excess" />

      <button type="submit">Submit</button>
    </form>
  </main>
</template>
