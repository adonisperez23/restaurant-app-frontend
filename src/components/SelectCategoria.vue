<template>
    <v-row justify="center">
        <p class="mr-2">Filtrar:</p>
        <select
            @change="(e:Event)=>{
            selectElement = e.target as HTMLSelectElement;
            $emit('change',selectElement.value)
            selectElement.value = 'Seleccionar'
        }"
        >
            <option
                v-for="categoria in [
                    'Seleccionar',
                    'Almuerzos',
                    'Bebidas',
                    'Zonas delivery',
                    'Extras',
                ]"
            >
                {{ categoria }}
            </option>
        </select>
    </v-row>
</template>

<script setup lang="ts">
import { ref } from "vue";

defineProps<{
    categoria: string;
}>();

const selectElement = ref<HTMLSelectElement>();

const $emit = defineEmits<{
    change: (value: string) => void;
}>();
</script>

<style scoped></style>
