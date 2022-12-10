<template>
  <div class="contentListGeneratedPage">
    <!-- Fonts -->
    <div class="importFontPoppins">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    </div>

    <div class="importFontInter">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Inter:wght@700&display=swap" rel="stylesheet">
    </div>
    <!-- Header -->
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

    <!-- Content Page -->
    <div class="backgroundScreen configFontPage">
      <h1>INÍCIO</h1>
      <div class="listSection">
        <div class="listBox">
            <h3>MINHA LISTA</h3>
            <div class="dividerList"></div>

              <nuxtIconNothing v-show="existItem"/>

          <div class="scrollItems">
            <ul>
              <li id="itemStyle" class="itemStyle" v-for="listGenerated in itemGenerated" :key="listGenerated">
                <div v-bind:id="(checkboxBackground + listGenerated.id)" class="checkboxBox" @click="activeCheckbox(listGenerated.id)">
                  <img v-bind:id="(checkboxIcon + listGenerated.id)" class="checkboxIcon" src="@/assets/finishList.svg" alt="Icone de Feito">
                </div>
                <p class="descriptionItem" v-bind:id="(descriptionItem + listGenerated.id)">{{ listGenerated.listInfo }}</p>
                <p id="typeItem">{{ listGenerated.listType }}</p>                
              </li>
            </ul>
          </div>
        </div>
      </div>
      <alertBugsApp />

      <button id="createList"><NuxtLink to="/createNewItem">CRIAR LISTA</NuxtLink></button>
    </div>
    
    <div>
      <slot />
    </div>

  </div>
</template>

<script>
  import "@/assets/styles/headerStyle.css";
  import "@/assets/styles/fonts/poppins.css";
  import "@/assets/styles/listBox.css"
  import "@/assets/styles/backgroundScreen.css"
  import "@/assets/styles/checkboxStyle.css"
  import "@/assets/styles/buttonStyle.css"

  import nuxtIconNothing from "@/components/nuxtIconNothing.vue"
  import alertBugsApp from "@/components/alertBugsApp.vue"

  export default {
    components: {
      nuxtIconNothing,
      alertBugsApp
    },
    data() {
      return {
        itemGenerated: null,
        existItem: false,
        descriptionItem: "descriptionItem",
        checkboxBackground: "checkboxBackground",
        checkboxIcon: "checkboxIcon"
      }
    },
    methods: {
      async getItems() {
        const req = await fetch("http://localhost:2000/listGenerated")
        const data = await req.json()
        this.itemGenerated = data
        if(this.itemGenerated[0] != null) {
          this.existItem = false
        } else {
          this.existItem = true
        }
      },
      activeCheckbox(id) {
        if(this.itemGenerated[id - 1].finish == false) {
          this.itemGenerated[id - 1].finish = true
          document.getElementById(`checkboxBackground${id}`).style.backgroundColor = "#00DC82"
          document.getElementById(`checkboxBackground${id}`).style.border = "3px solid #00DC82"
          document.getElementById(`checkboxIcon${id}`).style.display = "flex"

          document.getElementById(`descriptionItem${id}`).style.color = "#ffffff75"
          document.getElementById(`descriptionItem${id}`).style.textDecorationLine = "line-through"
        } else {
          this.itemGenerated[id - 1].finish = false
          document.getElementById(`checkboxBackground${id}`).style.backgroundColor = "#00DC8200"
          document.getElementById(`checkboxBackground${id}`).style.border = "3px solid #fff"
          document.getElementById(`checkboxIcon${id}`).style.display = "none"

          document.getElementById(`descriptionItem${id}`).style.color = "#ffffff"
          document.getElementById(`descriptionItem${id}`).style.textDecorationLine = "none"
        }
      },
      /* async sendStatusItem() {
        e.preventDefault();
        
        const data = {
          finish: this.checkboxActive
        }
        const dataJson = JSON.stringify(data)
        const req = await fetch(`http://localhost:2000/listGenerated/${id}`, {
          method: "FETCH",
          headers: {"Content-Type": "application/json"},
          body: dataJson
        })
      } */
    },
    mounted() {
      this.getItems()
    }
  }
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }

  /* Content Page */
  .configFontPage h1,
  .configFontPage h3,
  .configFontPage p {
    font-family: 'Poppins', sans-serif !important;
  }
  .configFontPage h1 {
    display: flex;
    position: absolute;
    top: 10vh;
    margin-bottom: 5vh;
    color: #fff;
  }
  
  .listSection {
    display: flex;
    flex-direction: column;

    position: absolute;
    top: 25vh;

    justify-content: center;
    align-items: center;
  }

  .contentListGeneratedPage {
    display: flex;
    flex-direction: column;

    justify-content: center;
    align-items: center;
  }

  /* Style Items */
  .itemStyle {
    display: flex;
    flex-direction: row;
    justify-items: center;
    align-items: center;
    margin: 10px;
  }
  .descriptionItem {
    margin-left: 10px;
    margin-right: 10px;
    color: #fff;
    transition: ease-in-out 250ms;
  }
  #typeItem {
    color: #ffffff75;
  }

  /* Ajust List Box */

  .scrollItems {
    width: 80% !important;
    height: auto;
    max-height: 250px !important;
    overflow-y: scroll;
    margin-top: 15px;
    margin-bottom: 15px;
  }
  .scrollItems::-webkit-scrollbar {
    width: 5px;
    background: #00DC8220;
    border-radius: 5px;
  }
  .scrollItems::-webkit-scrollbar-thumb {
    background: #00DC82;
    border-radius: 5px;
  }
</style>