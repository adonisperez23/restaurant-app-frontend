<template>
    <v-container style="max-width: 1200px">
        <BarraProgresoAviso
            v-if="cargandoLista"
            mensajeBarra="Cargando . . ."
            mensaje="Mostrando Menu ..."
            noMostrarAlert
        />
        <v-row v-if="listaVacia" justify="center">
            <v-sheet color="#f9cf57" rounded>
                <h1>No hay menu publicado por los momentos...</h1>
            </v-sheet>
            <v-col align="center" cols="6">
                <v-icon color="red" size="100">
                    mdi-server-food-variant-off
                </v-icon>
            </v-col>
        </v-row>
        <v-row v-if="errorDeCarga" justify="center">
            <v-sheet color="#f9cf57" rounded>
                <h1>
                    Ha ocurrido un error al cargar lista de menu...
                    <br />
                    ¡Posibles problemas con el servidor!
                    <br />
                    Lo sentimos...
                    <br />
                </h1>
            </v-sheet>
            <v-col align="center" cols="6">
                <v-icon color="red" size="100"> mdi-server-network-off </v-icon>
            </v-col>
        </v-row>
        <v-row v-if="listaAlmuerzos.length > 0" justify="start">
            <v-container>
                <SelectCategoria
                    :categoria="categoriaSeleccionada"
                    @change="iraCategoria"
                />

                <v-row justify="center">
                    <h2 class="px-5" id="Almuerzos">
                        <v-icon start icon="mdi-pasta"></v-icon>
                        Almuerzos
                    </h2>
                </v-row>
                <v-row justify="start">
                    <InfoMenu
                        v-for="(producto, index) in listaAlmuerzos"
                        :key="producto.id"
                        v-bind="producto"
                    />
                </v-row>
            </v-container>
        </v-row>
        <v-row v-if="listaBebidas.length > 0">
            <v-container>
                <SelectCategoria
                    :categoria="categoriaSeleccionada"
                    @change="iraCategoria"
                />
                <v-row justify="center">
                    <h2 class="px-5" id="Bebidas">
                        <v-icon start icon="mdi-beer"></v-icon>
                        Bebidas
                    </h2>
                </v-row>
                <v-row justify="start">
                    <InfoMenu
                        v-for="(producto, index) in listaBebidas"
                        :key="producto.id"
                        v-bind="producto"
                    />
                </v-row>
            </v-container>
        </v-row>
        <v-row v-if="listaRaciones.length > 0" justify="start">
            <v-container>
                <SelectCategoria
                    :categoria="categoriaSeleccionada"
                    @change="iraCategoria"
                />
                <v-row justify="center">
                    <h2 class="px-5" id="Extras">
                        <v-icon
                            start
                            icon="mdi-food-takeout-box-outline"
                        ></v-icon>
                        Extras
                    </h2>
                </v-row>
                <v-row justify="start">
                    <InfoMenu
                        v-for="(producto, index) in listaRaciones"
                        :key="producto.id"
                        v-bind="producto"
                    />
                </v-row>
            </v-container>
        </v-row>
        <v-row v-if="listaDelivery.length > 0">
            <v-container>
                <SelectCategoria
                    :categoria="categoriaSeleccionada"
                    @change="iraCategoria"
                />
                <v-row justify="center">
                    <h2 class="px-5" id="Zonas delivery">
                        <v-icon start icon="mdi-truck-delivery"></v-icon>
                        Zonas delivery
                    </h2>
                </v-row>
                <v-row justify="start">
                    <InfoMenu
                        v-for="(producto, index) in listaDelivery"
                        :key="producto.id"
                        v-bind="producto"
                    />
                </v-row>
            </v-container>
        </v-row>
    </v-container>
</template>

<script setup lang="ts">
import InfoMenu from "../components/menu/InfoMenu.vue";
import { ref, reactive, onMounted, provide } from "vue";
import axios from "axios";
import type { AxiosError, AxiosResponse } from "axios";
import type { Producto } from "../types/interfaces";
import BarraProgresoAviso from "../components/BarraProgresoAviso.vue";
import SelectCategoria from "@/components/SelectCategoria.vue";

let listaProductos = ref<Producto[]>([]); // Variable que almacena todos los productos de la base de datos
const cargandoLista = ref<boolean>(true); //Variable que activa la BarraProgresoAviso cuando se hace la llamada a la api
const listaVacia = ref<boolean>(false); // Controla el escrito cuando la lista de productos esta vacia o hay algun error en la llamada
const errorDeCarga = ref<boolean>(false);
const listaAlmuerzos = reactive<Producto[]>([]); //Variable que almacena solo los productos con categoria Almuerzo
const listaBebidas = reactive<Producto[]>([]); //Variable que almacena solo los productos con categoria Bebida
const listaRaciones = reactive<Producto[]>([]); //Variable que almacena solo los productos con categoria Racion
const listaDelivery = reactive<Producto[]>([]); //Variable que almacena solo los productos con categoria Delivery
// const listaFiltrada = listaMenu.value.filter(producto => producto.categoria === "Almuerzo" || producto.categoria === "Raciones")
const categoriaSeleccionada = ref("Almuerzos");

function iraCategoria(value: string) {
    categoriaSeleccionada.value = value;
    const element = document.getElementById(value);
    if (element) {
        element.scrollIntoView({ behavior: "smooth", block: "center" });
    }
}

ObtenerMenu();

provide("listaMenu", listaProductos); // provee a todos los componentes hijos de la lista de productos luego de realizar la llamada a la api

function ObtenerMenu(): void {
    axios
        .get(import.meta.env.VITE_API_LISTA_DE_PRODUCTOS)
        .then((res: AxiosResponse) => {
            setTimeout(() => {
                listaProductos.value = res.data;
                listaProductos.value.forEach((producto) => {
                    if (producto.disponible) {
                        switch (producto.categoria) {
                            case "Almuerzo":
                                listaAlmuerzos.push(producto);
                                break;
                            case "Bebida":
                                listaBebidas.push(producto);
                                break;
                            case "Racion":
                                listaRaciones.push(producto);
                                break;
                            case "Delivery":
                                listaDelivery.push(producto);
                                break;
                        }
                    }
                });
                estaListaVacia(listaProductos.value);
                cargandoLista.value = false;
                // console.log("lista filtrada", listaAlmuerzos,listaBebidas,listaRaciones)
            }, 2000);
            // console.log("lista Productos", res.data.listaMenu)
        })
        .catch((err: AxiosError) => {
            setTimeout(() => {
                cargandoLista.value = false;
                errorDeCarga.value = true;
            }, 2000);
            // console.log("error",err.response.data.error)
        });
}

function estaListaVacia(lista: Producto[]) {
    if (lista.length > 0) return (listaVacia.value = false);
    return (listaVacia.value = true);
}
</script>

<style scoped>
h2 {
    background-color: #f9cf57;
    border-radius: 5px;
}
</style>
