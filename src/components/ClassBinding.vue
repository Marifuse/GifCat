<template>
    <div>
        <!-- Cabecera de la Página -->
        <header class="cat-header">
            <h1>Random Gif Cat (⁎˃ᆺ˂)♥</h1>
        </header>
        <!-- Sección del formilario -->
        <section>
            <form class="form">
            <div class="input">   
              <label>Título: </label>
              <input type="text" v-model= 'cat.title'>
            </div>
            <div class="input">
              <label>Filtro: </label>
              <select name="Seleccione" id="" @change="filterChange($event)">
                <option value="blur">Blur</option>
                <option value="mono">Mono</option>
                <option value="sepia">Sepia</option>
                <option value="negative">Negative</option>
                <option value="paint">Paint</option>
                <option value="pixel">Pixel</option>
              </select>
            </div>
            <div class="input">
              <label>Color: </label>
              <select name="Seleccione" id="" @change="colorChange($event)">
                  <option value="green">Verde</option>
                  <option value="yellow">Amarillo</option>
                  <option value="red">Rojo</option>
                  <option value="blue">Azul</option>
                  <option value="black">Negro</option>
                  <option value="white">Blanco</option>
              </select>
            </div>
                <div class="input">
                  <label>Tamaño: </label>
                  <input type="text" v-model="cat.size">
                </div>
            </form>
        </section> 
         <!-- Sección de resultados -->
        <section class="cat-result">
            <button class="cat-search" @click="search">Obtener mi Gato</button>
            <br><br>
            <span v-show="cat.isLoading">Buscando Gato...</span>
            <img v-show="!cat.isLoading" :src="cat.src" alt="">
        </section>   
    </div>
</template>

<script>
export default {
  data() {
    return {
      cat: {
        src:'',  
        title: '',
        filter: '',
        color: '',
        size: '',
        isLoading: false    
       }
      }
    },
    methods: {
    search(){
      //ocultar foto y mostrar msj
      this.cat.isLoading = true
      fetch(`https://cataas.com/cat/gif/says/${this.cat.title}?filter=${this.cat.filter}&color=${this.cat.color}&size=${this.cat.size}`)
      .then(response => this.cat.src = response.url )
      //mostrar foto y ocultar mensaje 
      .then(() => this.cat.isLoading = false)
    },
    filterChange(event){
       this.cat.filter = event.target.value
    },
    colorChange(event){
       this.cat.color = event.target.value
    }
  },                                        
  computed:{
    title(){
       return this.cat.title;
    }
  }
}
</script>

<style>
    body {
        background-color: skyblue;
        font-family: 'Chelsea Market', cursive;
        text-align: center;
        margin: 0;
    }
    /* Cabecera */
    .cat-header {
        padding: 2em;
    }
    /* Formulario */
    .form {
        background-color: lightcoral;
        padding: 2em;
    }
    .input {
        padding: 1em;
    }
    .cat-search {
        background-color: lightcoral;
        font-weight: 900;
        padding: 1em;
        border-radius: 2em;
        border: 1px solid black;
        transition: 2s;
    }
    .cat-search:hover {
        background-color: #FFFFFF;
        color: #000000;
    }
    /* Sección resultado */
    .cat-result {
        padding: 2em;
    } 
</style>
