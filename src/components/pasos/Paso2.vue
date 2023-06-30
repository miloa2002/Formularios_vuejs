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

const emailTouched = ref(false);
const passwordTouched = ref(false);
const password2Touched = ref(false);
const telTouched = ref(false);
const celTouched = ref(false);

/*email*/
const showErrorEmail = computed(() => {
    return props.formData.email === '' && emailTouched.value;
});
const handleInputEmail = () => {
    emailTouched.value = true;
};

/*password*/
const showErrorPassword = computed(() => {
    return props.formData.password === '' && passwordTouched.value;
});
const handleInputPassword = () => {
    passwordTouched.value = true;
};

/*password2*/
const showErrorPassword2 = computed(() => {
    return props.formData.password2 === '' && password2Touched.value;
});
const handleInputPassword2 = () => {
    password2Touched.value = true;
};

/*tel*/
const showErrorTel = computed(() => {
    return props.formData.tel === '' && telTouched.value;
});
const handleInputTel = () => {
    telTouched.value = true;
};

/*cel*/
const showErrorCel = computed(() => {
    return props.formData.cel === '' && celTouched.value;
});
const handleInputCel = () => {
    celTouched.value = true;
};


</script>

<template>
    <div class="text-left mx-auto bg-white shadow-md rounded-md py-10 px-5 mb-10">

         <Alerta
                v-if="alerta.msg"
                :alerta="alerta" 
            />

        <div class="mb-5">
            <label for="email" class="block text-gray-700 font-bold">
                Escribe tu correo electrónico:
            </label>
            <div class="relative">
                <input type="email" id="email" placeholder="Email"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.email"
                    @change="handleInputEmail">
                <div v-if="showErrorEmail">
                    <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                </div>
                <div v-if="props.formData.email.length > 1">
                    <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                </div>
            </div>
        </div>

        <div class="md:flex items-center gap-4">
            <div class="mb-5 md:w-1/2">
                <label for="password" class="block text-gray-700 font-bold">
                    Escribe tu contraseña:
                </label>
                <div class="relative">
                    <input type="password" id="password" placeholder="Contraseña"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.password"
                        @change="handleInputPassword">

                    <div v-if="showErrorPassword">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.password.length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>

            <div class="mb-5 md:w-1/2">
                <label for="password2" class="block text-gray-700 font-bold">
                    Repite tu contraseña:
                </label>
                <div class="relative">
                    <input type="password" id="password2" placeholder="Repite contraseña"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.password2"
                        @change="handleInputPassword2">

                    <div v-if="showErrorPassword2">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.password2.length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>
        </div>

        <div class="md:flex items-center gap-4">
            <div class="mb-5 md:w-1/2">
                <label for="tel" class="block text-gray-700 font-bold">
                    Escribe tu número de teléfono :
                </label>
                <div class="relative">
                    <input type="tel" id="tel" placeholder="Teléfono "
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.tel"
                        @change="handleInputTel">

                    <div v-if="showErrorTel">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.tel.toString().length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>

            <div class="mb-5 md:w-1/2">
                <label for="tel2" class="block text-gray-700 font-bold">
                    Escribe tu número de celular:
                </label>
                <div class="relative">
                    <input type="tel" id="tel2" placeholder="Celular"
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" v-model="props.formData.cel"
                        @change="handleInputCel">

                    <div v-if="showErrorCel">
                        <i class="absolute right-8 top-5 text-red-500 fas fa-exclamation-circle"></i>
                    </div>
                    <div v-if="props.formData.cel.toString().length > 1">
                        <i class="absolute right-8 top-5 text-green-500 fas fa-check-circle"></i>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>