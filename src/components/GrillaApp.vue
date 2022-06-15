<template>
  <div>
    <SearchBar />
    <table class="table">
      <thead>
        <tr>
          <th class="col">Provincia</th>
          <th class="col">Abreviatura</th>
          <th class="col">Bandera</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr></tr>
        <tr v-for="provincia in provincias" :key="provincia.id">
          <td>{{ provincia.nombre }}</td>
          <td>{{ provincia.abreviatura }}</td>
          <td>
            <img :src="'/images/' + provincia.bandera" />
          </td>
          <td>
            <router-link
              class="btn btn-success"
              :to="{ name: 'provincia', params: { id: provincia.id } }"
            >
              Detalle
            </router-link>
            <router-link
              class="btn btn-primary"
              :to="{ name: 'formulario', params: { id: provincia.id } }"
            >
              Modificar
            </router-link>
            <button class="btn btn-danger" @click="eliminar(provincia.id)">
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'GrillaApp',
  props: {
    msg: String,
  },
  data() {
    return {
      provincias: [],
    }
  },
  mounted() {
    this.getProvincias()
  },
  methods: {
    async getProvincias() {
      const response = await fetch(
        'http://168.194.207.98:8081/api_provincia/get_provincias.php'
      )
      const data = await response.json()
      this.provincias = data
    },
    async eliminar(id) {
      await fetch(
        `http://168.194.207.98:8081/api_provincia/get_provincia.php?id=${id}`,
        {
          method: 'DELETE',
          headers: {
            'Content-type': 'application/json',
            'Access-Control-Allow-Origin': '*',
          },
          mode: 'cors',
        }
      )
      window.location.reload()
    },
  },
}
</script>
