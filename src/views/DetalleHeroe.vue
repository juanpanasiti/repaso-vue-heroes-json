<template>
  <div class="">
    <navigation-bar v-on:buscar="filtrar"> </navigation-bar>

    <h1>{{ heroeEncontrado.nombre }} - ({{ heroeEncontrado.casa }})</h1>

    <b-container fluid>
      <b-row>
        <br />
        <b-col cols="7" style="border-right: 1px solid #cecece">
          <div>
            <b-img
              :src="'/img/' + heroeEncontrado.img"
              fluid
              alt="Fluid image"
              style="height: 300px"
              center
            />
          </div>
          <p>
            <strong>BIO: </strong>
            {{ heroeEncontrado.bio }}
          </p>
        </b-col>

        <b-col cols="5" style="padding-top: 20px">
          <h1>{{ heroeEncontrado.nombre }}</h1>
          <h3><strong>CASA</strong> {{ heroeEncontrado.casa }}</h3>
          <h4>Poderes</h4>
          <ul v-for="poder in heroeEncontrado.poderes" :key="poder">
            <li>{{ poder }}</li>
          </ul>

          <p>
            <strong>1° aparición: </strong>
            {{ heroeEncontrado.aparicion }}
          </p>
          <br />
          <a href="javascript:history.go(-1)" class="btn btn-warning">
            Volver
          </a>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Navigation from "@/components/shared/Navigation.vue";

export default {
  name: "DetalleHeroe",
  props: [],
  components: {
    "navigation-bar": Navigation,
  }, //components

  mounted() {
    this.getHeroeXId();
  }, //mounted()

  data() {
    return {
      heroeEncontrado: [],
    };
  }, //data()

  methods: {
    async getHeroeXId() {
      const parametroId = this.$route.params.id;
      const res = await fetch("/heroes.json");
      const resJson = await res.json();
      this.heroeEncontrado = await resJson.find(
        (heroe) => heroe.id === parametroId
      );
    },
  }, //methods:
}; //export default
</script>

<style>
/*Los estilos en CSS (o LESS o lo que sea)*/
</style>
