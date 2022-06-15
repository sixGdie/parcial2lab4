<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container-fluid">
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0"></ul>
        <form class="d-flex">
          <input
            v-model="termino"
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
            id="busq"
          />
          <a class="btn btn-primary" :href="'/buscar/' + termino" role="button"
            >Buscar</a
          >
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',

  data() {
    return {
      termino: '',
    }
  },
}
</script>
