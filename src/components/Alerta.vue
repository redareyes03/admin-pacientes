<script setup>
import { computed } from 'vue';

const props = defineProps({
    alerta: {
        type: Object,
        required: true 
    }
})

const alertas = {
    error: () => "bg-red-500",
    exito: () => "bg-green-500"
}

const tipo = computed(() => {
    return alertas[props.alerta.tipo]()
})
</script>

<template>
    <div
    :class="tipo"
    class="text-white text-center p-3 uppercase font-bold mt-3 rounded-md">
    {{ alerta.mensaje }}</div>
</template>