<script setup>
import { reactive, ref } from 'vue';
import Header from './components/Header.vue';
import Paso1 from "./components/pasos/Paso1.vue"
import Paso2 from './components/pasos/Paso2.vue';
import Paso3 from './components/pasos/Paso3.vue';
import Swal from 'sweetalert2';

const alerta = reactive({
  tipo: "",
  msg: ""
})


const paso = ref(1);
const pasos = ['Paso1', 'Paso2', 'Paso3'];
const formData = ref({
  pais: "",
  genero: "",
  nombre: "",
  segundo_nombre: "",
  genero: "",
  fecha: "",
  tipo_documento: "",
  numero_documento: "",
  password: "",
  password2: "",
  tel: "",
  cel: "",
  email: "",
  direccion: "",
  postal: ""
});
const componenteActual = ref(pasos[0]); // El primer paso está visible inicialmente

const nextStep = () => {
  if (Object.values(formData.value).slice(0, 7).some((value, index) => index !== 3 && value === '')) {
    alerta.msg = "Todos los campos son obligatorios"
    alerta.tipo = "error"
    return;
  } else if (formData.value.numero_documento.toString().length <= 5) {
    alerta.msg = "El número del documento debe contener más o igual de 5 números"
    alerta.tipo = "error"
    return;
  }

  if (componenteActual.value === 'Paso2' && (formData.value.password === '' || formData.value.password2 === '' || formData.value.tel === '' || formData.value.cel === '' || formData.value.email === '')) {
    alerta.msg = "Todos los campos son obligatorios"
    alerta.tipo = "error"
    return;
  }

  if (componenteActual.value === 'Paso2' && (formData.value.password !==  formData.value.password2)) {
    alerta.msg = "Las contraseñas no coinciden"
    alerta.tipo = "error"
    return;
  }


  if (paso.value < pasos.length) {
    paso.value++;
    componenteActual.value = pasos[paso.value - 1];
  }
};

const prevStep = () => {
  if (paso.value > 1) {
    paso.value--;
    componenteActual.value = pasos[paso.value - 1];
  }
};

const submitForm = () => {
  if (componenteActual.value === 'Paso3' && (formData.value.direccion === '' || formData.value.postal === '')) {
    alerta.msg = "Todos los campos son obligatorios"
    alerta.tipo = "error"
    return;
  }

  Swal.fire({
    title: 'Confirmación',
    html: `
    <h4>Datos del formulario enviados señor@: ${formData.value.nombre}</h4>
  `,
    icon: 'info',
    showCancelButton: true,
    confirmButtonText: 'Sí',
    cancelButtonText: 'No'
  }).then((result) => {
    if (result.isConfirmed) {
      // La acción confirmada
    } else if (result.dismiss === Swal.DismissReason.cancel) {
      // La acción cancelada
    }
  });

  console.log(formData.value);

};

const getStepClass = (index) => {
  if (index + 1 === paso.value) {
    return 'w-4 h-4 bg-indigo-600 rounded-full';
  } else if (index + 1 < paso.value) {
    return 'w-4 h-4 bg-black rounded-full';
  } else {
    return 'w-4 h-4 bg-gray-300 rounded-full';
  }
};
</script>

<template>
  <div class="container mx-auto my-20">
    <Header />

    <div class="mt-12 p-8 md:p-0 md:w-1/2 mx-auto text-center">
      <div class="flex items-center justify-between mb-12">
        <div v-for="(step, index) in pasos" :key="index" class="flex items-center">
          <div :class="getStepClass(index)"></div>
          <span class="ml-2 font-medium">{{ step }}</span>
        </div>
      </div>

      <div v-if="componenteActual === 'Paso1'">
        <h2 class="text-2xl font-bold mb-12">Paso 1: Información personal</h2>
        <!-- Campos del Paso 1 -->
        <Paso1 :formData="formData" :alerta="alerta"/>
        <button @click="nextStep"
          class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-colors">Siguiente</button>
      </div>

      <div v-if="componenteActual === 'Paso2'">
        <h2 class="text-2xl font-bold mb-12">Paso 2: Detalles de contacto</h2>
        <!-- Campos del Paso 2 -->
        <Paso2 :formData="formData" :alerta="alerta"/>
        <button @click="nextStep"
          class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-colors">Siguiente</button>
        <button @click="prevStep" class="ml-2 text-blue-500 mt-4">Volver</button>
      </div>

      <div v-if="componenteActual === 'Paso3'">
        <h2 class="text-2xl font-bold mb-12">Paso 3: Confirmación</h2>
        <!-- Campos del Paso 3 -->
        <Paso3 :formData="formData" :alerta="alerta"/>
        <button @click="submitForm"
          class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-800 cursor-pointer transition-colors">Enviar</button>
        <button @click="prevStep" class="ml-2 text-blue-500 mt-4">Volver</button>
      </div>
    </div>
  </div>
</template>
