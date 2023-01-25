<template>
  <div class="container mt-3 text-white flex flex-col items-center">
    <p class="w-[700px] text-center">
      Є багатовимірний об'єкт, який формується динамічно при кожному запиті.
      Необхідно написати функцію, яка перетворить його в плоский формат.
      Врахувати правила найменування ключів: - якщо об'єкт дочірній, то в
      результаті ім'я ключа повинно містити ключі всіх об'єктів (не масивів)
      батьків у порядку вкладеності; - масиви залишаються масивами, якщо вони
      містять лише примітиви.
    </p>
    <div class="my-5">
      <div>
        <label
          for="message"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Object</label
        >
        <textarea
          id="message"
          class="w-[500px] h-[300px] block p-2.5 text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Write your thoughts here..."
          v-model="textArea"
        ></textarea>
      </div>
      <p>
        <button
          class="bg-white text-black rounded px-2 py-1 mt-1"
          @click.prevent="flattenObject(JSON.parse(textArea))"
        >
          Перетворити у плоский формат
        </button>
      </p>
    </div>
    <p>{{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
const result = ref("");
const multidimensionalObject = ref({
  User: 1,
  Data: {
    FirstName: "Anonymous",
    LastName: "AnonymousLastName",
    MiddleName: "AnonymousMiddleName",
    Role: [
      1,
      2,
      4,
      {
        isOwner: true,
      },
      {
        hidden: null,
      },
      {
        visibleStat: "null",
      },
    ],
  },
  Profile: [
    {
      Check: true,
      CheckRole: [1, 2, 34],
    },
    {
      Settings: {
        Rider: [1, 2, 3, 4],
        Inside: {
          In: true,
          Out: null,
        },
      },
    },
  ],
});
const textArea = ref(JSON.stringify(multidimensionalObject.value));
function flattenObject(obj, parentKey = "", flattenedObject = {}) {
  for (const key in obj) {
    if (typeof obj[key] === "object") {
      if (Array.isArray(obj[key])) {
        flattenedObject[`${parentKey}${key}`] = obj[key];
      } else {
        flattenObject(obj[key], `${parentKey}${key}.`, flattenedObject);
      }
    } else {
      flattenedObject[`${parentKey}${key}`] = obj[key];
    }
  }
  result.value = JSON.stringify(flattenedObject);
}
</script>

<style scoped></style>
