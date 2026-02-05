<script setup>
import { ref } from 'vue'

const usuario = ref({
  nombre: '',
  edad: null,
  bio: '',
  preferencias: {
    nivel: '',
    intereses: [],
    pais: '',
    tecnologias: []
  }
})

</script>

<template>
  <main class="container my-4">
    <h1>Registro de Perfil de Usuario</h1>
    <form>
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3">
        <div class="col">
          <div class="mb-3">
            <label for="nombre" class="form-label">Nombre</label>
            <input type="text" class="form-control" name="nombre" id="nombre" v-model="usuario.nombre">
          </div>
          <div class="mb-3">
            <label for="edad" class="form-label">Edad</label>
            <input type="number" class="form-control" name="edad" id="edad" v-model.number="usuario.edad">
          </div>
          <div class="mb-3">
            <label for="bio" class="form-label">Biografía</label>
            <textarea type="text" class="form-control" name="bio" id="bio" v-model.lazy="usuario.bio"></textarea>
          </div>
        </div>
        <div class="col"></div>
        <div class="col"></div>
      </div>
    </form>
  </main>

</template>

<style scoped></style>
