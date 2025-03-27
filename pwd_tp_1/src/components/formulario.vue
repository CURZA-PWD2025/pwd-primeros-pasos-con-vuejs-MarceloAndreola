<script setup lang="ts">
import { ref, computed } from 'vue'

defineProps<{ msg?: string }>()

const nombre = ref("")
const apellido = ref("")
const email = ref("")
const password = ref("")
const datetime = ref("")

function guardarDatos(){
    let usuario = {
        nombre: nombre.value,
        apellido: apellido.value,
        email: email.value,
        password: password.value,
        datetime: datetime.value
    }
    console.log(usuario)
    alert("Enviado correctamente")

}

function limpiarForm(){
    nombre.value = "";
    apellido.value = "";
    email.value = "";
    password.value = "";
    datetime.value = "";
}

const edad = computed(() => {
    if (!datetime.value) return null;

    let [año,mes,dia] = datetime.value.split("-").map(Number);

    let fechaNacimiento = new Date(año, mes - 1, dia);
    let hoy = new Date();

    let edadCalculada = hoy.getFullYear() - fechaNacimiento.getFullYear();
    
    return edadCalculada;
});

</script>

<template>
    <h1>{{ msg }}</h1>
    <div class="form">
        <div class="form_text">
            <input type="text" placeholder="nombre" v-model="nombre">
            <input type="text" placeholder="apellido" v-model="apellido">
            <input type="email" placeholder="email" v-model="email">
            <input type="password" placeholder="password" v-model="password">
            <input type="date" placeholder="fecha" v-model="datetime">
        </div>
        <button type="button" @click="guardarDatos">enviar</button>
        <button type="button" @click="limpiarForm">limpiar</button>
    </div>
    <div class="text">
        <p>Nombre: {{ nombre }}</p>
        <p>Apellido: {{ apellido }}</p>
        <p>Email: {{ email }}</p>
        <p v-if="edad !== null">Edad: {{ edad }}</p>
    </div>

</template>

<style scoped>
    h1{
        background-color:burlywood;
        border-radius: 10px;
    }

    .form{
        background-color:cornflowerblue;
        border-radius: 10px;
        margin: 50px 0;
        padding: 20px 20px;
    }

    .form_text{
        display: flex;
        flex-direction: column;
        margin-bottom: 10px;
    }

    button{
        background-color:deepskyblue;
        margin: 0 10px;
    }

    .text{
        background-color: cornflowerblue;
        padding: 20px 0;
        border-radius: 10px;
    }
</style>
