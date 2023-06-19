<script setup>
import { reactive } from 'vue';
    
    const paciente = reactive({
        nombre : ''
    })
</script>

<template>
    <div class="md:w-1/2">
       
        <p class="font-black text-3xl text-center">Seguimiento pacientes</p>
        <p class="text-lg mt-5 text-center mb-10 ">
            Añade pacientes y
            <span class="font-bold text-indigo-600">Administralos</span>
        </p>

        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10">
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
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none">
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
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none">
            </div>
            <div class="mb-5">
                <label 
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold">
                    Sintomas
                </label>

                <textarea
                id="sintomas"
                class="border-2 w-full mt-2 p-2 placeholder-gray-400 rounded-md outline-none resize-none h-30" />
            </div>

            <input 
            type="submit"
            class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
            value="registrar paciente">
        </form>
    </div>
</template>