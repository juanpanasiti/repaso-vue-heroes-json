<template>
  <div class="home">
    <navigation-bar v-on:buscar="filtrar">
    </navigation-bar>
    <div v-for="heroe in heroesData" :key="heroe.id">
      <hr />
      <heroe-item :heroeParam="heroe"></heroe-item>
    </div>
  </div>
</template>

<script>
import Heroe from "@/components/Heroe.vue";
import Navigation from "@/components/shared/Navigation.vue";
export default {
  name: "ListaHeroes",
  components: {
    "heroe-item": Heroe,
    "navigation-bar": Navigation
  }, //components

  mounted() {
    this.getHeroes();
  }, //mounted()

  data() {
    return {
      heroesData: [],
    };
  }, //data()

  methods: {
    //acá se definen los métodos que pueden ser llamados en cualquier momento

    async getHeroes() {
      const res = await fetch("/heroes.json");
      const resJson = await res.json();
        try {
          const casaParam = this.$route.params.casa.toUpperCase();
          for (let heroe of resJson) {
          if (heroe.casa.toUpperCase() === casaParam) {
            this.heroesData.push(heroe);
          }
        }
        } catch (error) {
         console.log(error);
          this.heroesData = resJson
        }
    },
    async filtrar(payload){
      await this.getHeroes()
      if(payload.busqueda.length == 0){
        console.log("Mostrar todo");
      } else {
        console.log("filtrar");
        let newHeroesData = []
        for(let heroe of this.heroesData){
          if(this.checkInclude(payload.busqueda,heroe)){
            newHeroesData.push(heroe)
          }
        }//for
        this.heroesData = newHeroesData
      }
    },//filtrar
    checkInclude(busqueda, heroe){

      const busq = busqueda.toLowerCase()
      const nombre = heroe.nombre.toLowerCase()
      const bio = heroe.bio.toLowerCase()
      const poderes = heroe.poderes
      if(nombre.includes(busq)){
        return true
      }
      if(bio.includes(busq)){
        return true
      }
      for(let poder of poderes){
        if (poder.toLowerCase().includes(busq)) {
          return true
        }
      }
      return false
    }//checkInclude()
  }, //methods:
}; //export default
</script>
