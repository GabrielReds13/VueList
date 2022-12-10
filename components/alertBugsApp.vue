<template>
  <div id="alertAction" class="alertAction" v-show="visible">
    <p id="descriptionAlert">&#8226;Este app está na <span>BETA 0.01,</span><br>
      logo, problemas podem ocorrer.</p>
  </div>
</template>

<script>
  import "@/assets/styles/fonts/poppins.css"
  import "@/assets/styles/alertActionStyle.css"
  export default {
    name: "alertBugsApp",
    data() {
      return {
        visible: true
      }
    },
    methods: {
      async renderingAlert() {
        setTimeout(() => this.visible = false, 8000)
      }
    },
    mounted() {
      this.renderingAlert()
    }
  }
</script>

<style scoped>
  .alertAction {
    position: absolute;
    z-index: 500;
    transform: translateY(22vh);
    transition: ease-in-out 250ms;
    background-color: #dc001d !important;
  }
  .alertAction p {
    color: #fff;
  }
  .alertAction span {
    font-weight: bold;
  }
</style>