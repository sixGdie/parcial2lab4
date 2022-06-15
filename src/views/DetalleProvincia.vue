<template>
  <div>
    <p>Provincia: {{ provincia.nombre }}</p>
    <p>Abreviatura: {{ provincia.abreviatura }}</p>
    <p>Capital: {{ provincia.capital }}</p>
    <p>Bandera: <img :src="'/images/' + provincia.bandera" /></p>
    <p>Población: {{ provincia.poblacion }}</p>
    <p>Superficie: {{ provincia.superficie }}</p>
    <p>N° Departamentos: {{ provincia.nroDepartamentos }}</p>
  </div>
</template>

<script>
export default {
  name: 'DetalleProvincia',
  components: {},
  mounted() {
    this.getProvincia()
  },
  data() {
    return {
      provincia: [],
    }
  },
  methods: {
    async getProvincia() {
      const res = await fetch(
        `http://168.194.207.98:8081/api_provincia/get_provincia.php?id=${this.$route.params.id}`
      )
      const data = await res.json()
      this.provincia = data
    },
  },
}
</script>
