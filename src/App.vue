<script setup lang="ts">
import { reactive, computed, ref } from "vue";
import RadioButtons from "./components/radio-buttons.vue";
import StartDateSelector from "./components/start-date-selector.vue";
import InsuredItems from "./components/insured-items.vue";
import LimitSelect from "./components/limit-select.vue";

const form = reactive({
  name: "" as string,
  items: [""] as string[],
  insureItems: true as boolean,
  startDate: "" as string,
  limitOfIndemnity: "" as string,
  excess: "" as string,
});

const excessOptions = [
  { value: "250", name: "excess" },
  { value: "500", name: "excess" },
  { value: "1000", name: "excess" },
];

const insureItemsOptions = [
  { value: "Yes", name: "insureItems" },
  { value: "No", name: "insureItems" },
];

const limitOptions = [
  { value: "1000000", label: "£1,000,000" },
  { value: "2000000", label: "£2,000,000" },
  { value: "5000000", label: "£5,000,000" },
];

const updateInsureItems = (value: string) => {
  form.insureItems = value === "Yes" ? true : false;
  if (!form.insureItems) {
    form.items = [""];
  }
};

const userCanSubmit = computed((): boolean => {
  return !!(
    form.name &&
    form.startDate &&
    form.limitOfIndemnity &&
    form.excess &&
    (form.insureItems ? form.items.every((item) => item.trim() !== "") : true)
  );
});

const userSubmitted = ref(false);

const completePolicy = () => {
  console.log(form);
  userSubmitted.value = true;
};
</script>

<template>
  <main
    class="align-center flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4"
  >
    <h1
      class="text-3xl font-bold text-center bg-gradient-to-r from-purple-600 to-orange-500 text-transparent bg-clip-text mb-6"
    >
      Insurance Policy
    </h1>
    <form
      @submit.prevent="completePolicy()"
      v-if="!userSubmitted"
      class="bg-white max-w-md w-full rounded-2xl shadow-xl p-8 space-y-6 text-gray-800"
    >
      <div>
        <h2 class="text-xl font-semibold border-b-2 mb-4">Customer</h2>
        <label for="name" class="block text-md font-semibold mb-1">Name</label>
        <input
          id="name"
          v-model="form.name"
          placeholder="Enter name"
          required
          type="text"
          class="w-full rounded-lg border border-gray-300 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
      </div>

      <div>
        <h2 class="text-xl font-semibold border-b-2 mb-4">Items</h2>

        <RadioButtons
          :radioOptions="insureItemsOptions"
          legendText="Do you want to insure items?"
          @radio-updated="updateInsureItems"
          :checked="form.insureItems === true ? 'Yes' : 'No'"
        />

        <InsuredItems v-model:items="form.items" v-if="form.insureItems" />
      </div>

      <div>
        <h2 class="text-xl font-semibold border-b-2 mb-4">Policy</h2>
        <StartDateSelector @date-updated="form.startDate = $event" />
      </div>

      <LimitSelect
        :selected="form.limitOfIndemnity"
        :options="limitOptions"
        @limit-updated="form.limitOfIndemnity = $event"
      />

      <RadioButtons
        :radioOptions="excessOptions"
        legendText="Excess"
        @radio-updated="form.excess = $event"
        :checked="form.excess"
      />

      <button
        type="submit"
        :disabled="!userCanSubmit"
        class="w-full py-3 mt-4 bg-gradient-to-r from-purple-600 to-orange-500 text-white rounded-xl text-lg font-semibold hover:brightness-110 transition disabled:opacity-50 cursor-pointer"
      >
        Submit
      </button>
    </form>
    <div v-else>
      <h2
        class="text-3xl font-bold text-center bg-gradient-to-r from-purple-600 to-orange-500 text-transparent bg-clip-text"
      >
        Thank you for your submission!
      </h2>
    </div>
  </main>
</template>
