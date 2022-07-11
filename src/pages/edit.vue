<script setup="" lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

const { push } = useRouter();

const tasksTeks = ref("");

if (localStorage.tasksTeks) {
  tasksTeks.value = localStorage.tasksTeks;
}

function simpan() {
  localStorage.tasksTeks = tasksTeks.value;
  localStorage.tasksList = JSON.stringify(
    tasksTeks.value
      .split("\n")
      .filter((x) => x)
      .map((x) => x.replace(/^\- /, ""))
  );
  push("/");
}
</script>

<template>
  <section class="wadah">
    <h1>Edit Tasks</h1>
    <form action="" @submit.prevent="simpan">
      <textarea
        name=""
        required
        id=""
        cols="30"
        rows="10"
        placeholder="first task
second task
third task"
        v-model="tasksTeks"
      ></textarea>
      <input type="submit" value="Done" />
    </form>
  </section>
</template>

<style>
[v-cloak] {
  @apply hidden;
}

* {
  @apply break-words;
}

.wadah {
  @apply p-5 pb-10;
}

.wadah h1 {
  @apply text-center text-3xl pb-5;
}

textarea {
  @apply border focus: outline-none border-gray-300 px-2 py-1 rounded w-full;
}

[type="submit"] {
  @apply w-full bg-white px-3 py-1 rounded border border-gray-400 text-gray-700 cursor-pointer focus: (bg-black text-white) hover: (bg-black text-white);
}
</style>
