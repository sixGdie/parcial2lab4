<template>
  <div style="max-width: 75%; padding-left: 25%">
    <div class="mb-3">
      <label for="exampleFormControlInput1" class="form-label">Nombre</label>
      <input
        v-model="provincia.nombre"
        type="text"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Nombre"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput2" class="form-label">Capital</label>
      <input
        v-model="provincia.capital"
        type="text"
        class="form-control"
        id="exampleFormControlInput2"
        placeholder="Capital"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput3" class="form-label">Poblacion</label>
      <input
        v-model="provincia.poblacion"
        type="text"
        class="form-control"
        id="exampleFormControlInput3"
        placeholder="Poblacion"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput4" class="form-label"
        >Superficie</label
      >
      <input
        v-model="provincia.superficie"
        type="text"
        class="form-control"
        id="exampleFormControlInput7"
        placeholder="Superficie"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput5" class="form-label"
        >N° Departamentos</label
      >
      <input
        v-model="provincia.nroDepartamentos"
        type="number"
        class="form-control"
        id="exampleFormControlInput4"
        placeholder="N° Departamentos"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput6" class="form-label"
        >Abreviatura</label
      >
      <input
        v-model="provincia.abreviatura"
        type="text"
        class="form-control"
        id="exampleFormControlInput5"
        placeholder="Abreviatura"
        required
      />
    </div>
    <div class="mb-3">
      <label for="exampleFormControlInput7" class="form-label">Bandera</label>
      <input
        v-model="provincia.bandera"
        type="text"
        class="form-control"
        id="exampleFormControlInput6"
        placeholder="Bandera"
        required
      />
    </div>
    <div class="col-auto">
      <button
        type="button"
        @click="guardar(provincia)"
        class="btn btn-primary mb-3"
      >
        Guardar
      </button>
    </div>
  </div>
</template>

<script>
import router from '@/router'
import { defineComponent, onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
export default defineComponent({
  name: 'FormularioInstumento',
  components: {},
  setup() {
    const route = useRoute()
    const provincia = ref({
      nombre: '',
      capital: '',
      poblacion: '',
      superficie: '',
      nroDepartamentos: '',
      abreviatura: '',
      bandera: '',
    })
    onMounted(async () => {
      const id = route.params.id
      if (id != 0) {
        const res = await fetch(
          `http://168.194.207.98:8081/api_provincia/get_provincia.php?id=${route.params.id}`
        )
        const data = await res.json()
        provincia.value = data
      }
    })

    return {
      provincia: provincia,
    }
  },
  methods: {
    async guardar(provincia) {
      let url = 'http://168.194.207.98:8081/api_provincia/post_provincia.php'
      let method = 'POST'
      if (provincia && provincia.id > 0) {
        url =
          'http://168.194.207.98:8081/api_provincia/put_provincia.php' +
          provincia.id
        method = 'PUT'
      }
      await fetch(url, {
        method: method,
        body: JSON.stringify(provincia),
        headers: {
          'Content-Type': 'application/json',
        },
      })
      router.push('/')
    },
  },
})
</script>
