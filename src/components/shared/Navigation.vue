<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Modificar Titulo</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <a href="/" class="nav-link"> HOME </a>
          <a href="/dc" class="nav-link"> Héroes DC </a>
          <a href="/marvel" class="nav-link"> Héroes Marvel </a>
        </b-navbar-nav>

        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input size="sm" class="mr-sm-2" v-model="busqueda"></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" v-on:click="buscar()">
              Buscar
            </b-button>
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
  export default {
    name: 'Navigation',
    components: {
    },//components

    mounted(){
    },//mounted()

    data() {
      return {
      }
    },//data()

    methods: {
      buscar(){
        //window.location.href = "/busqueda/" + this.filter
        this.$emit('buscar', { busqueda: this.busqueda })
      }//buscar
    }//methods:
  }//export default
</script>