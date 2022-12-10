<template>
  <div>
    <div class="importFontInter">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Inter:wght@700&display=swap" rel="stylesheet">
    </div>
    <header>
      <!-- Menu Logo -->
      <div class="logoApp">
        <img src="@/assets/logoApp.svg" alt="VueList">
      </div>

      <!-- Menu Options -->
      <nav>
        <ul class="optionList">
          <li><p><NuxtLink to="/">LISTA</NuxtLink></p></li>
          <li><p><NuxtLink to="/options">OPCIONAIS</NuxtLink></p></li>
        </ul>
      </nav>
    </header>

    <div>
      <slot />
    </div>

  </div>
</template>

<script>
  import "@/assets/styles/headerStyle.css";
  import "@/assets/styles/fonts/inter.css";
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }
</style>