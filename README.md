# l3-ejercicio-binding-formularios

## Decisiones para Binding y validaciones

### Modificadores de v-model utilizados:

- **v-model**: Binding bidireccional estándar (nombre, edad)
- **v-model.number**: Convierte automáticamente el input a número (edad)
- **v-model.lazy**: Actualiza solo cuando el usuario sale del campo (biografía)

### Validaciones implementadas:

1. **Nombre** (requerido): Debe contener texto no vacío
2. **Edad** (requerida): Debe ser un número entre 1 y 120
3. **Intereses** (requerido): Debe seleccionar al menos una opción
4. Validación en tiempo real con eventos `@blur` y `@change`
5. El botón de envío se deshabilita si el formulario es inválido

## Capturas

### Captura del Formulario

### Captura del Panel de Resumen

## Sobre el Proyecto

### Contexto

Crear un formulario interactivo donde se ponga en práctica el 2-way binding de Vue con `v-model`.
Se utilizarán distintos tipos de input:

- text
- number
- textarea
- checkbox
- radio
- select

Se desarrollará un panel de resumen donde se mostrarán los cambios realizados en el formulario en tiempo real.

### Estructura de datos

El formulario servirá para la creación del perfil de un `usuario`. Que tendrá la siguiente estructura:

```javascript
{
  nombre: '',           // String: Nombre completo del usuario (requerido)
  edad: null,           // Number: Edad del usuario (1-120, requerido)
  bio: '',              // String: Biografía o descripción personal (opcional)
  preferencias: {
    nivel: '',          // String: Nivel de experiencia (Trainee, Junior, Semi Senior, Senior)
    intereses: [],      // Array: Lista de intereses seleccionados (requerido, mínimo 1)
    pais: '',           // Object: País seleccionado con código y nombre
    tecnologias: []     // Array: Tecnologías que maneja (múltiple)
  }
}
```

### Opciones disponibles:

**Niveles de Experiencia:**

- Trainee
- Junior
- Semi Senior
- Senior

**Intereses:**

- Programacion
- Hiking
- Gaming
- Cocina

**Países:**

- Chile (CL)
- Argentina (AR)
- México (MX)
- España (ES)
- Japón (JP)
- Canadá (CA)
- Australia (AU)
- Brasil (BR)
- Alemania (DE)
- Italia (IT)

**Tecnologías:**

- Vue
- React
- Angular
- Svelte
- Astro
- Nuxt

## Funcionalidades principales

1. **Formulario interactivo** con 6 tipos de inputs diferentes (text, number, textarea, radio, checkbox, select)
2. **2-way binding** en tiempo real con `v-model`
3. **Panel de resumen** que muestra los datos del formulario en vivo
4. **Validaciones reactivas** que se actualizan mientras el usuario escribe/selecciona
5. **Botón de envío** deshabilitado mientras el formulario sea inválido
6. Uso de **Composition API** de Vue 3 con `<script setup>`

## Tecnologías utilizadas

- **Vue 3**: Framework JavaScript progresivo
- **Vite**: Herramienta de build rápida y moderna
- **Bootstrap 5**: Framework CSS para estilos
- **ESLint**: Linter para mantener código limpio

## Instalación y Configuración

1. Clonar el repositorio
2. Instalar dependencias: `pnpm install` o `npm install`
3. Ejecutar en desarrollo: `pnpm dev` o `npm run dev`
4. El servidor estará disponible en `http://localhost:5173`, ahí podrás ver los cambios en tiempo real.

## Conceptos clave de Vue abordados

- **v-model**: Two-way data binding
- **computed()**: Propiedades reactivas calculadas
- **ref()**: Crea references reactivas
- **v-for**: Renderización de listas
- **v-if/v-show**: Renderización condicional
- **@click/@change/@blur**: Event listeners
- **:class/:value/:disabled**: Binding de atributos y propiedades
- **Métodos validación**: Validación en tiempo real con eventos`
