<script setup>
import { defineProps } from 'vue';
import { computed, ref } from 'vue';
import '@fortawesome/fontawesome-free/css/all.css'
import Alerta from '../Alerta.vue';

const props = defineProps({
    formData: {
        type: Object,
        required: true
    },
    alerta: {
        type: Object,
        required: false
    }
})

const dirTouched = ref(false);
const postalTouched = ref(false);


/*dir*/
const showErrorDir = computed(() => {
    return props.formData.direccion === '' && dirTouched.value;
});
const handleInputDir = () => {
    dirTouched.value = true;
};

/*postal*/
const showErrorPostal = computed(() => {
    return props.formData.postal === '' && postalTouched.value;
});
const handleInputPostal = () => {
    postalTouched.value = true;
};


</script>

<template>
    <div class="text-left mx-auto bg-white shadow-md rounded-md py-10 px-5 mb-10">

         <Alerta
                v-if="alerta.msg"
                :alerta="alerta" 
            />

        <div class="mb-5">
            <label for="direccion" class="block text-gray-700 font-bold">
                Escribe tu dirección residencia:
            </label>
            <div class="relative">
                <input type="text" id="direccion" placeholder="Dirección"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.direccion"
                    @change="handleInputDir">

                <div v-if="showErrorDir">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.direccion.length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

        <div class="mb-5">
            <label for="postal" class="block text-gray-700 font-bold">
                Escribe tu código postal:
            </label>
            <div class="relative">
                <input type="number" id="postal" placeholder="Código postal"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.postal"
                    @change="handleInputPostal">
                <div v-if="showErrorPostal">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.postal.toString().length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

    </div>
</template>