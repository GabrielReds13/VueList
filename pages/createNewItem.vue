<template>
  <div>
    <div class="importFontPoppins">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    </div>

    <div class="backgroundScreen">
      <h1>CRIAR LISTA</h1>

      <div class="createListSection configFontPage">
        <div class="list">
          <div class="listBox">
              <h3>MENU</h3>
              <alertAction :messageAlert="messageAlert" v-show="messageAlert"/>
              <div class="dividerList"></div>

              <form id="listStructure" @submit="createList">
                <!-- Insert Name List -->
                <input id="inputCharacter" class="inputCharacter" type="text" v-model="listInfo" placeholder="Nome da Lista">
                <div class="dividerList"></div>
                <!-- Insert Type List -->
                <select name="listType" id="listType" class="listType" v-model="listType">
                  <option value="" selected>Tipo da Lista</option>
                  <option v-for="ListType in typeLists" :key="ListType.id" :value="ListType.type">{{ ListType.type }}</option>
                </select>
                <button id="createList" type="submit"><p>CRIAR</p></button>
              </form>
          </div>

        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
  import "@/assets/styles/fonts/poppins.css"
  import "@/assets/styles/listBox.css"
  import "@/assets/styles/backgroundScreen.css"
  import "@/assets/styles/inputCharacter.css"
  import "@/assets/styles/listTypeStyle.css"
  import "@/assets/styles/buttonStyle.css"

  import alertAction from "@/components/alertAction.vue"

  export default {
    components: {
      alertAction
    },
    data() {
      return {
        typeLists: null,
        listInfo: null,
        listType: null,
        finish: false,
        messageAlert: null
      }
    },
    methods: {
      async getTypeLists() {
        const req = await fetch("http://localhost:2000/listType/")
        const data = await req.json()
        this.typeLists = data
      },
      async createList(form) {
        form.preventDefault()

        const data = {
          listInfo: this.listInfo,
          listType: this.listType,
          finish: this.finish
        }
        const dataJson = JSON.stringify(data)
        const req = await fetch("http://localhost:2000/listGenerated", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: dataJson
        })
        const res = await req.json()

        this.messageAlert = `Lista n°${res.id} criada com sucesso`

        setTimeout(() => {
          this.messageAlert = ""
        }, 3000)
        this.listInfo = null
        this.listType = null
      }
    },
    mounted() {
      this.getTypeLists()
    }
  }
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }

  /* Config Font Page */
  .backgroundScreen h1,
  .backgroundScreen h3,
  .backgroundScreen p {
    font-family: 'Poppins', sans-serif !important;
  }
  .backgroundScreen h1 {
    display: flex;
    position: absolute;
    top: 10vh;
    margin-bottom: 5vh;
    color: #fff;
  }
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

  /* Config Position Section */
  .createListSection {
    display: flex;
    flex-direction: column;

    position: absolute;
    top: 25vh;

    justify-content: center;
    align-items: center;
  }

  /* Divider Config */
  .dividerList {
    margin-bottom: 10px;
  }

  /* Ajust List Box */
  .listBox {
    height: 20vh;
  }

  /* Ajust Form */
  #listStructure {
    display: flex;
    flex-direction: column;
    width: 80%;
    justify-content: center;
    align-items: center;
  }

  /* Ajust Button */
  #createList {
    transform: translateY(45vh);
  }
</style>