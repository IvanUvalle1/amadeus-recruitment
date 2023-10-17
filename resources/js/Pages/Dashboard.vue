<!-- // Nombre -- Ivan de Jesus Uvalle Aguayo
Pues durante la prueba he sentido que algunas instrucciones no estuvieron claras para instalar el sistema
Algunos problemas que quiero destacar en el paso 4 primero se realiza composer install antes de php artisan key:generate,
el correo para acceder ya no es amadeus@amadeus.com es admin@amadeusmagister.com y se deberia comentar que se tiene que hacer la configuracion incial
-->
<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

const props = defineProps ({
    customroute: {
        type: String,
        default: () => "dashboard",
    },
    data: {
        type: Array,
        default: () => [],
    },
    events: {
        type: Array,
        default: () => [],
    },
});

</script>

<template>
    <Head title="Inicio" />

    <AuthenticatedLayout :croute="customroute">

        <div class="mx-auto">
            <div class="shadow-sm sm:rounded-lg amadeus-box">
                <div class="p-5">¡Bienvenido a Amadeus!</div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>

<style scoped>

.amadeus-box {
    background: #3C7FF8;
    border-radius: 2rem;
    font-size: 1.5rem;
	color: #fff;
    font-weight: 800;
    font-size: 2.5rem;
    text-align: center;
}

</style>