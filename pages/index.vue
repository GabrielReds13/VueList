<template>
  <div>
    <div class="importFontPoppins">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    </div>
  </div>
</template>

<script setup>
  import "@/assets/styles/fonts/poppins.css"

  definePageMeta({
    layout: 'groups'
  })
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }
</style>