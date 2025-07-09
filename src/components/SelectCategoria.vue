<template>
    <v-row justify="center">
        <p class="mr-2">Filtrar:</p>
        <select
            @change="(e:Event)=>{
            const selectElement = e.target as HTMLSelectElement;
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
defineProps<{
    categoria: string;
}>();

const $emit = defineEmits<{
    change: (value: string) => void;
}>();
</script>

<style scoped></style>
