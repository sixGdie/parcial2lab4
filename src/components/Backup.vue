<template>
  <div>
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
          <td><img :src="'assets/' + provincia.bandera" alt="" /></td>
          <td>
            <router-link
              :to="{ name: 'provincia', params: { id: provincia.id } }"
            >
              Detalle Modificar
            </router-link>
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
  methods: {
    getProvincias() {
      this.$http
        .get('http://168.194.207.98:8081/api_provincia/get_provincias.php')
        .then((response) => {
          this.provincias = response.data
        })
    },
  },
  data() {
    return {
      provincias: [],
    }
  },
}
</script>
