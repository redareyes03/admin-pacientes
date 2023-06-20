<script setup>
import { computed, reactive } from 'vue';
import Alerta from './Alerta.vue'
    

    const props = defineProps({
        mascota: {
            type: String,
            required: true
        },
        propietario: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        },
        modo: {
            type: String, 
            required: true
        },
        alerta: {
            type: Object,
            required: true
        }
    })


    const emit = defineEmits(['update:mascota', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente', 'modificar-modo', 'modificar-alerta' ])
    
    
    

    const validar = () => {
        if(Object.values(props).includes('')){
            emit('modificar-alerta', {
                mensaje : "Todos los campos son obligatorios",
                tipo : "error",
                display : true
            })
            setTimeout(() => emit('modificar-alerta', {...props.alerta, display: false}), 2000 )
            return
        }

        emit('guardar-paciente')

        if(props.modo === "editar"){
            emit('modificar-alerta', {
                mensaje : "Paciente actualizado!",
                tipo : "exito",
                display : true
            })
        }else{
            emit('modificar-alerta', {
                mensaje : "Paciente registrado!",
                tipo : "exito",
                display : true
            })
        }
        emit('modificar-modo', 'registrar')
        setTimeout(() => emit('modificar-alerta', {...props.alerta, display: false}), 2000 )
    }

</script>

<template>
    <div class="md:w-1/2">
       
        <p class="font-black text-3xl text-center">Seguimiento pacientes</p>
        <p class="text-lg mt-5 text-center mb-10 ">
            Añade pacientes y
            <span class="font-bold text-indigo-600">Administralos</span>
        </p>

        <form 
        class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
        @submit.prevent="validar">
            <div class="mb-5">
                <label 
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <input 
                type="text"
                id="mascota"
                placeholder="Nombre de la mascota"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none"
                :value="mascota"
                @input="$emit('update:mascota', $event.target.value)"
               >
            </div>

            <div class="mb-5">
                <label 
                    for="propietario"
                    class="block text-gray-700 uppercase font-bold">
                    Nombre propietario
                </label>
                
                <input 
                type="text"
                id="propietario"
                placeholder="Nombre del propietario"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none"
                :value="propietario"
                @input="$emit('update:propietario', $event.target.value)"
               >
            </div>

            <div class="mb-5">
                <label 
                    for="email"
                    class="block text-gray-700 uppercase font-bold">
                    Email
                </label>

                <input 
                type="email"
                id="email"
                placeholder="Email del propietario"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none"
                :value="email"
                @input="$emit('update:email', $event.target.value)"
               >
            </div>

            <div class="mb-5">
                <label 
                    for="alta"
                    class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>

                <input 
                type="date"
                id="alta"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none"
                :value="alta"
                @input="$emit('update:alta', $event.target.value)"
                >
            </div>

            <div class="mb-5">
                <label 
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>

                <textarea
                id="sintomas"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none resize-none h-30"
                :value="sintomas"
                @input="$emit('update:sintomas', $event.target.value)"
                />
            </div>

            <input 
            type="submit"
            class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
            :value="modo + ' paciente'">

            <Alerta 
            v-if="alerta.display"
            :alerta="alerta"/> 
        </form>
    </div>
</template>