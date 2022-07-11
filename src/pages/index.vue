<script setup="" lang="ts">
import { ref } from "vue";
import Pensil from "../icon/pensil.vue";
import Info from "../komponen/info.vue";

const list = ref([]);
const nilai = ref(0);

if (localStorage.tasksList) {
  list.value = JSON.parse(localStorage.tasksList);

  let tanggalan = new Date();
  let tanggalSekarang = tanggalan.getDate();
  let banyakList = list.value.length;

  if (tanggalSekarang >= banyakList) {
    nilai.value = tanggalSekarang % banyakList;
  } else {
    nilai.value = banyakList % tanggalSekarang;
  }
}
</script>

<template>
  <Info></Info>
  <section class="wadah">
    <h1>My Tasks</h1>
    <ol class="app">
      <li v-for="(x, n) in list" :class="n == nilai ? 'terpilih' : ''">
        {{ x }}
      </li>
    </ol>
  </section>
  <router-link class="tombol kanan" to="/edit">
    <Pensil></Pensil>
  </router-link>
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

.app li {
  @apply px-2 py-1 inline-block rounded mr-1 mb-1 text-sm border border-gray-300;
}

.terpilih {
  /*ini buat style yang terpilih*/
  @apply bg-black text-white border-black;
}

.wadah h1 {
  @apply text-center text-3xl pb-5;
}

.tombol.kiri {
  @apply left-0;
}

.tombol.kanan {
  @apply right-0;
}
</style>
