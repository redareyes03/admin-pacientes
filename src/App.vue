<script setup>
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import { ref, reactive} from 'vue';

const paciente = reactive({
  mascota: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

const pacientes = ref([])
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario
      v-model:mascota="paciente.mascota"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas" />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="pacientes.length"></div>
        <div v-else>
          <h2 class="text-center text-2xl mt-20">No hay pacientes</h2>
        </div>
      </div>
    </div>
  </div>
</template>

