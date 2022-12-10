<template>
  <div id="alertAction" class="alertAction alertSucceful">
    <p id="descriptionAlert">&#8226;{{ messageAlert }}.</p>
  </div>
</template>

<script>
  import "@/assets/styles/fonts/poppins.css"
  import "@/assets/styles/alertActionStyle.css"
  export default {
    name: "alertAction",
    props: {
      messageAlert: String
    },
  }
</script>

<style>
  .alertAction {
    position: absolute;
    z-index: 500;
    transform: translateY(22vh);
    transition: ease-in-out 250ms;
  }
  .alertSucceful {
    background-color: #00DC82 !important;
  }
</style>