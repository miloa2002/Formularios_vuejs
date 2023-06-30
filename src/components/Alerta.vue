<script setup>
const props = defineProps({
    alerta: {
        type: Object,
        required: false
    }
})

</script>


<template>
    <div
        class="text-white text-center p-3 font-bold mb-8 rounded-md bg-red-600"
    >
        {{ alerta.msg }}
    </div>
</template>
