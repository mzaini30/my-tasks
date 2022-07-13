<script setup="" lang="ts">
import { ref } from "vue";
import Pensil from "../icon/pensil.vue";
import Info from "../komponen/info.vue";

const { stringify, parse } = JSON;

const list = ref([]);
const nilai = ref(0);

function sekarang(): string {
  const tanggalan = new Date();
  const tanggal = tanggalan.getDate();
  const bulan = tanggalan.getMonth() + 1;
  return `${tanggal}/${bulan}`;
}

if (localStorage.tasksList) {
  list.value = parse(localStorage.tasksList);

  let tanggalan = new Date();
  let tanggalSekarang = tanggalan.getDate();
  let banyakList = list.value.length;

  if (tanggalSekarang >= banyakList) {
    nilai.value = tanggalSekarang % banyakList;
  } else {
    nilai.value = banyakList % tanggalSekarang;
  }

  if (localStorage.aktif) {
    const aktif = parse(localStorage.aktif);
    if (aktif.tanggal === sekarang()) {
      nilai.value = aktif.posisi;
    }
  }
}

function ubah(n: number) {
  nilai.value = n;

  localStorage.aktif = stringify({
    tanggal: sekarang(),
    posisi: n,
  });
}
</script>

<template>
  <Info></Info>
  <section class="wadah">
    <h1>My Tasks</h1>
    <ol class="app">
      <li
        v-for="(x, n) in list"
        class="cursor-pointer select-none"
        @click="ubah(n)"
        :class="n == nilai ? 'terpilih' : ''"
      >
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
