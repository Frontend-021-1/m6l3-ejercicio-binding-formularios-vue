<script setup>
import { ref, computed } from 'vue'

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

const handleSubmit = () => {
  console.log(`%cEnviando datos de: ${usuario.value.nombre}`, 'background-color:teal;color:white;padding:5px;border-radius:5px')
  console.log(usuario.value)
}

// Validaciones
const isNameInvalid = computed(() => {
  const nombre = usuario.value.nombre
  return !nombre || nombre === ''
})

const isAgeInvalid = computed(() => {
  const edad = usuario.value.edad
  return !edad || edad <= 0 || edad > 120
})

const isInteresInvalid = computed(() => !usuario.value.preferencias.intereses.length)

const ageError = ref(false)
const nameError = ref(false)
const interesError = ref(false)

const ageValidation = () => ageError.value = isAgeInvalid.value
const nameValidation = () => nameError.value = isNameInvalid.value
const interesValidation = () => interesError.value = isInteresInvalid.value

const isFormInvalid = computed(() => isAgeInvalid.value || isNameInvalid.value || isInteresInvalid.value)
</script>

<template>
  <main class="container my-4">
    <h1>Registro de Perfil de Usuario</h1>
    <form @submit.prevent="handleSubmit">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3">
        <div class="col">
          <div class="mb-3">
            <label for="nombre" class="form-label">Nombre</label>
            <input type="text" class="form-control" :class="{ 'border-danger': nameError }" name="nombre" id="nombre"
              v-model="usuario.nombre" @blur="nameValidation">
            <p class="text-danger error-text" v-show="nameError">⚠︎ Nombre es obligatorio</p>
          </div>
          <div class="mb-3">
            <label for="edad" class="form-label">Edad</label>
            <input type="number" class="form-control" :class="{ 'border-danger': ageError }" name="edad" id="edad"
              v-model.number="usuario.edad" @blur="ageValidation">
            <p class="text-danger error-text" v-show="ageError">⚠︎ Edad es obligatoria y debe estar entre 1 y 120</p>

          </div>
          <div class="mb-3">
            <label for="bio" class="form-label">Biografía</label>
            <textarea type="text" class="form-control" name="bio" id="bio" v-model.lazy="usuario.bio"></textarea>
            <p class="form-text">{{ usuario.bio.length }}</p>
          </div>
        </div>
        <div class="col">
          <!-- Nivel de experiencia: radio button group -->
          <div class="mb-3">
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
          </div>

          <!-- Intereses: check group -->
          <div class="mb-3">
            <fieldset>
              <legend class="h6">Intereses</legend>
              <div class="form-check" v-for="interes in intereses" :key="interes">
                <input class="form-check-input" type="checkbox" :value="interes" :name="interes" :id="interes"
                  v-model="usuario.preferencias.intereses" @change="interesValidation">
                <label class="form-check-label" :for="interes">
                  {{ interes }}
                </label>
                <p class="text-danger error-text" v-show="interesError">⚠︎ Debes seleccionar al menos un interés</p>
              </div>
            </fieldset>
          </div>
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
      <div class="text-center d-grid d-md-block">
        <button type="submit" class="btn btn-primary" :disabled="isFormInvalid">Enviar datos</button>
      </div>
    </form>

    <hr class="my-5">

    <!-- Sección Panel de Resumen -->
    <div class="card text-center">
      <div class="card-header">
        Resumen de datos del usuario
      </div>
      <div class="card-body">
        <h5 class="card-title">{{ usuario.nombre }}</h5>
        <h6 class="card-subtitle">Edad: {{ usuario.edad }}</h6>
        <p class="card-text">Desarrollador nivel {{ usuario.preferencias.nivel }}</p>
        <div class="row row-cols-1 row-cols-md-2">
          <div class="col text-start">
            <p class="fw-bold">Interesado en:</p>
            <ul class="list-group ">
              <li class="list-group-item" v-for="interes in usuario.preferencias.intereses">{{ interes }}</li>
            </ul>
          </div>
          <div class="col text-start">
            <p class="fw-bold">Tecnologías que maneja:</p>
            <ul class="list-group ">
              <li class="list-group-item" v-for="tec in usuario.preferencias.tecnologias">{{ tec }}</li>
            </ul>
          </div>
        </div>
      </div>
      <div class="card-footer text-body-secondary">
        País: {{ usuario.preferencias.pais.nombre }}
      </div>
    </div>
  </main>

</template>

<style scoped>
.error-text {
  font-size: 12px;
}
</style>
