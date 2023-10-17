<template>
    <Head title="Inventario" />

    <AuthenticatedLayout :croute="customroute">

        <div class="mx-auto">
            Lista de inventario
            <div v-for="(item, index) in items" :key="item.id" @click="showDetails(item)">
                <div :class="getShadowColorClass(item.status)" class="shadow-sm sm:rounded-lg amadeus-box">
                    <div class="p-5">
                        <div class="info-container">
                            <div class="info-left">
                                <i class="fa fa-music"></i>
                                &nbsp;&nbsp;{{ item.type }} <span class="blue-text"> <span class="bold-text">{{ item.name
                                }}</span> </span>{{ item.brand }}
                            </div>
                            <div class="info-right">
                                <span class="status-text">{{ item.status }} </span>
                                <span class="status-icon">
                                    <i :class="getStatusIconClass(item.status)"></i>
                                </span>
                            </div>
                        </div>
                    </div>
                    <div v-if="itemDetails && itemDetails.id === item.id" class="details">
                        <p>Modelo: {{ item.model }}</p>
                        <p>Número de serie: {{ item.serialNumber }}</p>
                        <p>Observaciones: {{ item.observations }}</p>
                        <div class="button-container">
                            <button type="button" class="btn btn-outline-primary">
                                Historial Prestamos <i class="fa fa-plus"></i>
                            </button>
                            <button type="button" class="btn btn-outline-primary">
                                Historial Reparaciones <i class="fa fa-plus"></i>
                            </button>
                            <button type="button" class="btn btn-outline-primary">
                                Realizar Prestamo <i class="fa fa-plus"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const props = defineProps({
    customroute: {
        type: String,
        default: () => "inventory.show",
    },
    items: {
        type: Array,
        default: () => [],
    },
    loan_agreement: {
        type: String,
        default: () => "",
    },
});

const itemDetails = ref(null);

function showDetails(item) {
    itemDetails.value = item;
}

function getShadowColorClass(status) {
    switch (status) {
        case "Disponible":
            return "color-green";
        case "Prestamo":
            return "color-orange";
        case "Reparación":
            return "color-red";
        case "No disponible":
            return "color-black";
        default:
            return "color-default"; // Puedes definir una clase de estilo predeterminada si es necesario
    }
}

function getStatusIconClass(status) {
    switch (status) {
        case "Disponible":
            return "fa fa-check-circle green-icon";
        case "Prestamo":
            return "fa fa-times-circle yellow-orange";
        case "Reparación":
            return "fa fa-exclamation-triangle red-icon";
        case "No disponible":
            return "fa fa-exclamation-circle black-icon";
        default:
            return ""; // No se muestra ningún icono para estados no reconocidos
    }
}
</script>

<style scoped>
/* Define clases CSS para las sombras de color */
.color-green {
    border-bottom: 5px solid green;
    /* Cambia el grosor de la línea según lo desees */
}

.color-orange {
    border-bottom: 5px solid orange;
    /* Cambia el grosor de la línea según lo desees */
}

.color-red {
    border-bottom: 5px solid red;
    /* Cambia el grosor de la línea según lo desees */
}

.color-black {
    border-bottom: 5px solid black;
    /* Cambia el grosor de la línea según lo desees */
}

/* Estilo para la clase predeterminada (puedes personalizarla según tus necesidades) */
.color-default {
    border-bottom: 5px solid gray;
    /* Cambia el grosor de la línea según lo desees */
}

/* Clases para los iconos de estado */
.green-icon {
    color: green;
    /* Cambia el color del icono a verde */
}

.yellow-orange {
    color: orange;
    /* Cambia el color del icono a amarillo */
}

.red-icon {
    color: red;
    /* Cambia el color del icono a rojo */
}

.black-icon {
    color: black;
    /* Cambia el color del icono a negro */
}

.blue-text {
    color: blue;
    /* Cambia el color del texto a azul */
}

.bold-text {
    font-weight: bold;
    /* Hace el texto en negrita */
    border-radius: 10px;
    /* Aplica un borde redondeado al texto */
}

/* Estilo para los iconos de música */
.fa-music {
    /* Estilo para el ícono de música, si es necesario */
}

/* Estilo para la clase que alinea el texto a la derecha */
.item-info {
    text-align: right;
}

.status-icon {
    display: flex;
    align-items: center;
}

.info-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.info-left {
    display: flex;
    align-items: center;
}

.info-right {
    display: flex;
    align-items: center;
}

.status-icon {
    margin-right: 5px;
    /* Ajusta el margen entre el icono y el texto según tus necesidades */
}

.button-container {
    display: flex;
    gap: 10px; /* Espacio entre botones, ajusta según tus necesidades */
}

.button-container button {
    flex: 1; /* Los botones ocupan el espacio disponible */
}
</style>