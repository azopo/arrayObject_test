<template>
  <div class="container mt-3 text-white flex flex-col items-center">
    <p class="w-[700px] text-center">
      Є масив чисел, впорядкований за зростанням (наприклад,
      [-2,0,1,2,3,4,5,8,9,11,13,15,18,22,25,28,29,30]). Необхідно написати
      функцію, яка приймає такий масив і повертає рядок (String), в якому всі
      числа виведені через кому. Але якщо числа йдуть підряд, то вивести їх
      діапазоном через тире, наприклад 21,22,23,24 => 21-24. Приклад результату
      для масиву із задачі: "-2, 0-5, 8, 9, 11, 13, 15, 18, 22, 25, 28-30".
    </p>
    <div class="mt-10 flex">
      <div class="w-[500px] mr-2">
        <input
          placeholder="Введіть масив чисел"
          v-model="inputModel"
          class="w-full bg-white text-black rounded py-2 px-3 focus:outline-amber-50 focus:ring-0"
        />
        <p class="text-[14px] text-[#ababab]">
          Масив чисел через кому, або пробіл
        </p>
      </div>
      <p>
        <button
          class="bg-white text-black rounded px-2 py-1 mt-1"
          @click.prevent="rangeString"
        >
          Згенерувати рядок
        </button>
      </p>
    </div>
    <p>{{ result }}</p>
  </div>
</template>
<script setup>
import { ref } from "vue";

const arr = [
  -2, 0, 1, 2, 3, 4, 5, 8, 9, 11, 13, 15, 18, 22, 25, 28, 29, 30, 31,
];
const inputModel = ref(arr);
const result = ref("");
// function to convert a string of numbers separated by commas or spaces into a range string
const rangeString = () => {
  // split the input string into an array of numbers
  const arr = inputModel.value.toString().split(/,| /);
  // clear the result value if it has any previous value
  if (result.value.length > 0) {
    result.value = "";
  }
  // initialize the start and end values to the first element of the array
  let start = arr[0];
  let end = arr[0];

  // loop through the rest of the array
  for (let i = 1; i < arr.length; i++) {
    // if the current number is one more than the previous number
    if (arr[i] - arr[i - 1] === 1) {
      // update the end value
      end = arr[i];
    } else {
      // if the start and end values are the same, add the start value to the result
      result.value += start === end ? start : start + "-" + end;
      // add a comma and space to the result
      result.value += ", ";
      // update the start and end values to the current number
      start = arr[i];
      end = arr[i];
    }
  }

  // add the final range or single value to the result
  result.value += start === end ? start : start + "-" + end;
};
</script>
