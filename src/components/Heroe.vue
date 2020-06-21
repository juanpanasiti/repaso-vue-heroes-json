<template>
  <div class="">
    <table style="width:500px;" class="table table-bordered">
      <tr>
        <td style="color:green; font-weight: bold;">
          {{ heroeParam.nombre }}
        </td>
        <td style="color:red; font-weight: bold;">Poderes</td>
      </tr>
      <tr>
        <td>
          <img
            :src="'/img/' + heroeParam.img"
            class="card-img-top"
            alt="imagen de un superheroe"
          />
        </td>
        <td>
          <ul v-for="poder in heroeParam.poderes" :key="poder">
            <li>{{ poder }}</li>
          </ul>
        </td>
      </tr>
      <tr>
        <td>
          <router-link :to="'/detalle-heroe/' + heroeParam.id" class="btn btn-secondary">VER MAS</router-link>
        </td>
        <td></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Heroe",
  props: ["heroeParam"],
  components: {}, //components

  mounted() {}, //mounted()

  data() {
    return {};
  }, //data()

  methods: {}, //methods:
}; //export default
</script>

<style>
/*Los estilos en CSS (o LESS o lo que sea)*/
</style>
