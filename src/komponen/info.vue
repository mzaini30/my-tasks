<script setup="" lang="ts">
import { Ref, ref } from "vue";

const { stringify, parse } = JSON;

const isi: Ref<any> = ref({
  slug: "",
  judul: "",
});

if (localStorage.info) {
  isi.value = parse(localStorage.info);
}

async function ambilData() {
  let data = await fetch("https://android.zenia.my.id/pertama.json");
  data = await data.json();
  isi.value = data;
  localStorage.info = stringify(data);
}
ambilData();
</script>

<template>
  <div class="bg-black text-white truncate p-3 text-center text-sm">
    <a
      :href="`https://android.zenia.my.id/tulisan/${isi.slug}`"
      class="underline decoration-dotted"
      >{{ isi.judul }}</a
    >
  </div>
</template>
