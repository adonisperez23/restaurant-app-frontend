<template>
    <v-container
        style="max-width: 1200px"
        class="mt-1 pt-1 fondo-comida mobile"
    >
        <v-row class="mt-16 pt-16">
            <v-col class="mt-6 pt-6">
                <div class="text-center fondo-titulo">
                    <h1>Rest los cinco sabores</h1>
                    <h3>¡Ven y observa nuestro menu disponible!</h3>
                    <div>
                        <v-btn-toggle>
                            <v-btn href="#resumen" size="x-small" variant="text"
                                >Como usar la app</v-btn
                            >
                            <v-btn
                                href="#ubicacion"
                                size="x-small"
                                variant="text"
                                >Nuestra Ubicacion</v-btn
                            >
                            <v-btn
                                href="#contacto"
                                size="x-small"
                                variant="text"
                                >Contactos</v-btn
                            >
                        </v-btn-toggle>
                    </div>
                </div>
            </v-col>
        </v-row>
    </v-container>
    <ResumenApp id="resumen" />
    <Ubicacion id="ubicacion" />
    <Contacto id="contacto" />
    <TheFooter />
</template>

<script setup lang="ts">
import ResumenApp from "../components/home/ResumenApp.vue";
import Contacto from "../components/home/Contacto.vue";
import Ubicacion from "../components/home/Ubicacion.vue";
import TheFooter from "../components/home/TheFooter.vue";
</script>

<style scoped>
.fondo-comida {
    background-image: url("/fotos/fotocomida.webp");
    background-size: 1200px 560px;
    height: 560px;
    border: solid 5px orange;
    border-radius: 5px;
}
.fondo-titulo {
    background-color: #fcecd2;
    opacity: 0.7;
    border: solid 2px orange;
    border-radius: 5px;
}
@media (max-width: 400px) {
    .mobile {
        background-image: url("/fotos/mobilefoto.webp");
        background-size: 400px 660px;
        height: 660px;
        border-radius: 5px;
    }
}
</style>
