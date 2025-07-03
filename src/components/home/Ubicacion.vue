<template>
    <v-container class="mt-6 pt-6 mb-16 pb-16">
        <v-row class="mt-6 pt-6 mb-16 pb-16" justify="center">
            <v-col :cols="cols">
                <h2 class="px-3">Direccion:</h2>
                <p>
                    Avenida orinoco, en frente de Agencias Unidas de Automoviles
                    C.A
                </p>
                <iframe
                    src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d7864.66063757326!2d-63.1977622!3d9.7380618!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x8c334756c1aceb53%3A0x8658c5187bac443e!2sRest.%20Los%20Cinco%20Sabores%2C%20C.A!5e0!3m2!1ses!2sve!4v1751488446149!5m2!1ses!2sve"
                    width="600"
                    height="450"
                    :style="{ border: 0, maxWidth: mobile ? '350px' : '100%' }"
                    class="my-4"
                    loading="lazy"
                    referrerpolicy="no-referrer-when-downgrade"
                ></iframe>
                <v-img
                    class="borde-imagen"
                    width="400"
                    height="400"
                    aspect-ratio="1/1"
                    cover
                    src="/fotos/fachada-rest.webp"
                >
                </v-img>
                <!-- <v-btn
                    class="mt-3"
                    variant="tonal"
                    color="#f88905"
                    @click="abrirGoogleMaps"
                >
                    Ver ubicacion en Google maps
                </v-btn> -->
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup lang="ts">
import { inject, computed } from "vue";
import type { Ref } from "vue";

const mobile = inject("isMobile") as Ref;
const cols = computed<string>(() => {
    if (mobile.value) {
        return "12";
    } else {
        return "6";
    }
});

function abrirGoogleMaps() {
    window.open(
        "https://www.google.com/maps/place/Rest.+Los+Cinco+Sabores,+C.A/@9.7380618,-63.1977622,16.67z/data=!4m6!3m5!1s0x8c334756c1aceb53:0x8658c5187bac443e!8m2!3d9.7376674!4d-63.198623!16s%2Fg%2F11c2r43k51?authuser=0"
    );
}
</script>

<style lang="css" scoped>
h2 {
    background-color: #f3d595;
    display: inline;
    border-radius: 5px;
}
</style>
