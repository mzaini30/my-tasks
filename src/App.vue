<script setup="" lang="ts">
import Love from "./icon/love.vue";
</script>

<template>
  <router-view />
  <a
    class="tombol kiri"
    href="https://play.google.com/store/apps/details?id=com.mzaini30.mytasks"
  >
    <Love></Love>
  </a>
</template>

<style>
.tombol {
  @apply fixed bottom-0 p-2 text-3xl;
}

.tombol.kiri {
  @apply left-0;
}
</style>
