<template>
  <div>
    <div class="importFontPoppins">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    </div>

    <div class="nothingLogo">
      <img class="nothingIcon" src="@/assets/nuxtIcon.svg" alt="Logo do Nuxt">
      <p class="nothingText">Nada além <br> de montanhas</p>
    </div>
  </div>
</template>

<script>
  import "@/assets/styles/fonts/poppins.css";
  export default {
    name: "nuxtIconNothing"
  }
</script>

<style scoped>
  .nothingLogo {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 25px;
  }
  .nothingIcon {
    width: 75px;
    margin-bottom: 1vh;
  }
  .nothingText {
    font-family: "Poppins", sans-serif !important;
    font-weight: bold;
    text-align: center;
    line-height: 98%;
  }
</style>