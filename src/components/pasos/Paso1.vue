<script setup>
import { computed, ref } from 'vue';
import { defineProps } from 'vue';
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


setTimeout(() => {
    Alerta.remove()
}, 2000);


const nombreTouched = ref(false);
const paisTouched = ref(false);
const segundo_nombreTouched = ref(false);
const generoTouched = ref(false);
const fechaTouched = ref(false);
const documentoTouched = ref(false);
const documentoTouchedN = ref(false);

/*nombre*/
const showErrorNombre = computed(() => {
    return props.formData.nombre === '' && nombreTouched.value;
});
const handleInputNombre = () => {
    nombreTouched.value = true;
};

/*pais*/
const showErrorPais = computed(() => {
    return props.formData.pais === '' && paisTouched.value;
});
const handleInputPais = () => {
    paisTouched.value = true;
};

/*segundo nombre*/
const showErrorSegundoNombre = computed(() => {
    return props.formData.segundo_nombre === '' && segundo_nombreTouched.value;
});
const handleInputSegundoNombre = () => {
    segundo_nombreTouched.value = true;
};

/*género*/
const showErrorGenero = computed(() => {
    return props.formData.genero === '' && generoTouched.value;
});
const handleInputGenero = () => {
    generoTouched.value = true;
};

/*fecha nacimiento*/
const showErrorFecha = computed(() => {
    return props.formData.fecha === '' && fechaTouched.value;
});
const handleInputFecha = () => {
    fechaTouched.value = true;
};

/*documento*/
const showErrorDocumento = computed(() => {
    return props.formData.tipo_documento === '' && documentoTouched.value;
});
const handleInputDocumento = () => {
    documentoTouched.value = true;
};

/*n documento*/
const showErrorDocumentoN = computed(() => {
    return props.formData.numero_documento === '' && documentoTouchedN.value;
});
const handleInputDocumentoN = () => {
    documentoTouchedN.value = true;
};

</script>

<template>
    <div class="text-left mx-auto bg-white shadow-md rounded-md py-10 px-5 mb-10">

        <Alerta
            v-if="alerta.msg"
            :alerta="alerta" 
        />

        <div class="mb-5">
            <label for="pais" class="block text-gray-700 font-bold">
                Selecciona tu país:
            </label>
            <div class="relative">
                <select id="pais" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md text-gray-400"
                    v-model="props.formData.pais" @change="handleInputPais">
                    <option value="">---Selecciona tu país---</option>
                    <option value="colombia">Colombia</option>
                    <option value="argentina">Argentina</option>
                </select>
                <div v-if="showErrorPais">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.pais.length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

        <div class="md:flex items-center gap-4">
            <div class="mb-5 md:w-1/2">
                <label for="nombre" class="block text-gray-700 font-bold">
                    Escribe tu nombre:
                </label>
                <div class="relative">
                    <input type="text" id="nombre" placeholder="Nombre"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.nombre"
                        @input="handleInputNombre">
                    <div v-if="showErrorNombre">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.nombre.length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>

            <div class="mb-5 md:w-1/2">
                <label for="segundo_nombre" class="block text-gray-700 font-bold">
                    Escribe tu segundo nombre:
                </label>
                <div class="relative">
                    <input type="text" id="segundo_nombre" placeholder="Segundo nombre"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                        v-model="props.formData.segundo_nombre" @input="handleInputSegundoNombre">
                    <div v-if="showErrorSegundoNombre">
                        <i class="absolute right-3 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.segundo_nombre.length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>
        </div>

        <div class="mb-5">
            <label for="genero" class="block text-gray-700 font-bold">
                Selecciona tu género:
            </label>
            <div class="relative">
                <select id="genero" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md text-gray-400"
                    v-model="props.formData.genero" @change="handleInputGenero">
                    <option value="">---Selecciona tu género---</option>
                    <option value="colombia">Femenino</option>
                    <option value="argentina">Masculino</option>
                </select>
                <div v-if="showErrorGenero">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.genero.length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

        <div class="mb-5">
            <label for="fecha" class="block text-gray-700 font-bold">
                Selecciona tu fecha de nacimiento:
            </label>
            <div class="relative">
                <input type="date" id="fecha" class="border-2 w-full p-2 mt-2 rounded-md text-gray-400"
                    v-model="props.formData.fecha" @change="handleInputFecha">
                <div v-if="showErrorFecha">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.fecha.length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

        <div class="md:flex items-center gap-4">
            <div class="mb-5 md:w-1/2">
                <label for="tipo_documento" class="block text-gray-700 font-bold">
                    Tipo de documento:
                </label>
                <div class="relative">
                    <select id="tipo_documento"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md text-gray-400"
                        v-model="props.formData.tipo_documento" @change="handleInputDocumento">
                        <option value="">---Selecciona el tipo de documento---</option>
                        <option value="cedula_ciudadania">Cédula de ciudadanía</option>
                        <option value="cedula_extranjeria">Cédula de extranjería</option>
                        <option value="pasaporte">Pasaporte</option>
                    </select>
                    <div v-if="showErrorDocumento">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.tipo_documento.length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>

            <div class="mb-5 md:w-1/2">
                <label for="numero_documento" class="block text-gray-700 font-bold">
                    N de documento:
                </label>
                <div class="relative">
                    <input type="number" id="numero_documento" class="border-2 w-full p-2 mt-2 rounded-md text-gray-400"
                        placeholder="Escribe el número de documento" v-model="props.formData.numero_documento"
                        @input="handleInputDocumentoN">
                    <div v-if="showErrorDocumentoN">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.numero_documento.toString().length >= 5">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>
        </div>

        <!-- {/*inputs de las fotos*/} -->

    </div>
</template>