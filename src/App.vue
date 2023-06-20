<script setup>
import { ref, reactive} from 'vue';
import {v4 as uid} from 'uuid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/Paciente.vue'

const alerta = reactive({
    tipo: '',
    mensaje: '',
    display: false
})

const modificarAlerta = (nuevaAlerta) => Object.assign(alerta, nuevaAlerta);

const paciente = reactive({
  id: null,
  mascota: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
})

const pacientes = ref([])

const modo = ref('registrar')

const guardarPaciente = () => {
    if(paciente.id){ //Edit mode
      const indexToEdit = pacientes.value.findIndex(({id}) => id === paciente.id)
      pacientes.value[indexToEdit] = {...paciente}
    }else{
      pacientes.value.push({...paciente, id: uid()})
    }
    Object.assign(paciente, {
      id: '',
      mascota: '',
      propietario: '',
      email: '',
      alta: '',
      sintomas: ''
    })
}

const editarPaciente = (id) => {
  modo.value = 'editar'
  const pacienteEditar = pacientes.value.filter((paciente) => paciente.id === id)[0]
  Object.assign(paciente, pacienteEditar);
}

const eliminarPaciente = (id) => {
  pacientes.value = pacientes.value.filter(paciente => paciente.id !== id)
  modificarAlerta({
    mensaje: "Paciente eliminado!",
    tipo: "error",
    display: true
  })
  setTimeout(() => Object.assign(alerta, {...alerta, display: false}), 2000)
}

const modificarModo = (nuevoModo) => modo.value = nuevoModo
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
      :modo="modo"
      :alerta="alerta"
      @modificar-modo="modificarModo"
      @modificar-alerta="modificarAlerta"
      @guardar-paciente="guardarPaciente" />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <p class="text-lg mt-5 text-center mb-10 ">
            Informacion de
            <span class="font-bold text-indigo-600">Pacientes</span>
        </p>
        <div v-if="pacientes.length" v-for="infoPaciente in pacientes">
          <Paciente
          :paciente="infoPaciente"
          @editar-paciente="editarPaciente"
          @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <div v-else>
          <h2 class="text-center text-2xl mt-20">No hay pacientes</h2>
        </div>
      </div>
    </div>
  </div>
</template>

