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

const niveles = [
  'Trainee', 'Junior', 'Semi Senior', 'Senior'
]
const intereses = [
  'Programacion', 'Hiking', 'Gaming', 'Cocina'
]
const paises = [
  { code: 'CL', nombre: 'Chile' },
  { code: 'AR', nombre: 'Argentina' },
  { code: 'MX', nombre: 'México' },
  { code: 'ES', nombre: 'España' },
  { code: 'JP', nombre: 'Japón' },
  { code: 'CA', nombre: 'Canadá' },
  { code: 'AU', nombre: 'Australia' },
  { code: 'BR', nombre: 'Brasil' },
  { code: 'DE', nombre: 'Alemania' },
  { code: 'IT', nombre: 'Italia' }
]
const tecnologias = [
  'Vue', 'React', 'Angular', 'Svelte', 'Astro', 'Nuxt'
]

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
            <p class="form-text">{{ usuario.bio.length }}</p>
          </div>
        </div>
        <div class="col">
          <!-- Nivel de experiencia: radio button group -->
          <fieldset>
            <legend class="h6">Nivel de Experiencia</legend>
            <div class="form-check" v-for="nivel in niveles" :key="nivel">
              <input class="form-check-input" type="radio" :value="nivel" :name="nivel" :id="nivel"
                v-model="usuario.preferencias.nivel">
              <label class="form-check-label" :for="nivel">
                {{ nivel }}
              </label>
            </div>
          </fieldset>

          <!-- Intereses: check group -->
          <fieldset>
            <legend class="h6">Intereses</legend>
            <div class="form-check" v-for="interes in intereses" :key="interes">
              <input class="form-check-input" type="checkbox" :value="interes" :name="interes" :id="interes"
                v-model="usuario.preferencias.intereses">
              <label class="form-check-label" :for="interes">
                {{ interes }}
              </label>
            </div>
          </fieldset>
        </div>
        <div class="col">
          <!-- Select de países -->
          <div class="mb-3">
            <label for="pais">País</label>
            <select class="form-select" id="pais" name="pais" aria-label="Default select example"
              v-model="usuario.preferencias.pais">
              <option selected disabled>Selecciona un país</option>
              <option :value="pais" v-for="pais in paises" :key="pais.code">{{ pais.nombre }}</option>
            </select>
          </div>

          <!-- Select múltiple de tecnologías -->
          <div class="mb-3">
            <label for="tecnologias">Tecnologías</label>
            <select class="form-select" name="tecnologias" id="tecnologias" multiple
              aria-label="Multiple select example" v-model="usuario.preferencias.tecnologias">
              <option selected>Open this select menu</option>
              <option :value="tecnologia" v-for="tecnologia in tecnologias" :key="tecnologia">{{ tecnologia }}</option>
            </select>
          </div>
        </div>
      </div>
    </form>

    <hr class="my-5">

    <!-- Sección Panel de Resumen -->
    <div class="card text-center">
      <div class="card-header">
        Featured
      </div>
      <div class="card-body">
        <h5 class="card-title">Special title treatment</h5>
        <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
      <div class="card-footer text-body-secondary">
        2 days ago
      </div>
    </div>
  </main>

</template>

<style scoped></style>
