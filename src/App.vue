<script setup>
import { ref, reactive} from 'vue';
import {v4 as uid} from 'uuid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue'

const paciente = reactive({
  id: null,
  mascota: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

const pacientes = ref([])

const guardarPaciente = () => {
    pacientes.value.push({...paciente, id: uid()})
    Object.assign(paciente, {
    mascota: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  })
}

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
      v-model:sintomas="paciente.sintomas"
      @guardar-paciente="guardarPaciente" />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <p class="text-lg mt-5 text-center mb-10 ">
            Informacion de
            <span class="font-bold text-indigo-600">Pacientes</span>
        </p>
        <div v-if="pacientes.length" v-for="infoPaciente in pacientes">
          <Paciente
          :paciente="infoPaciente"/>
        </div>
        <div v-else>
          <h2 class="text-center text-2xl mt-20">No hay pacientes</h2>
        </div>
      </div>
    </div>
  </div>
</template>

