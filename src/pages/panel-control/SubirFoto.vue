<template>
  <v-container>
    <BarraProgresoAviso
    v-if="alert.mostrarAlert"
    mostrarAlert
    mensajeBarra="Cargando..."
    :colorAlert="alert.color"
    :iconoAlert="alert.icon"
    :mensajeAlert="alert.mensaje"
    />
    <v-row v-else justify="center">
      <v-col cols="12">
        <v-sheet width="300" class="mx-auto">
          <div v-show="mostrarFormulario" class="text-center">
            Cargar Imagen adjunta
            <v-text-field readonly label="Nombre del producto" v-model="route.query.nombreProducto"></v-text-field>
            <v-file-input v-model="imagen" label="Cargar Imagen"></v-file-input>
            <v-btn prepend-icon="mdi-upload" color="green" :disabled=" typeof imagen === 'undefined'" @click="subirFoto">{{cargandoFoto ? "Subiendo foto..." : "Subir Foto"}}</v-btn>
            <div class="text-center mt-1">
              <v-btn prepend-icon="mdi-image-album" color="blue" block  @click="nuevaFoto">Buscar nueva foto</v-btn>
              <h3 class="text-center">Nota:</h3>
              <p>Antes de cargar una imagen, verifique primero que el nombre del archivo solo contenga caracteres.
                La carga de la imagen no permite emoticones en su nombre.
              </p>
            </div>
          </div>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import {ref,reactive} from 'vue'
import {useRoute,useRouter} from 'vue-router'
import {useEstadoAlerta} from '../../stores/estadoAlerta'
import axios from 'axios'
import BarraProgresoAviso from '../../components/BarraProgresoAviso.vue'
import type {Foto} from '../../types/interfaces'
import type {AxiosError,AxiosResponse} from 'axios'

const alert = useEstadoAlerta()
const route = useRoute()
const router = useRouter()

const imagen = ref<File[]>()
const infoFoto = reactive<Foto>({
  nombreFoto:'',
  direccionUrl:'', // no esta siendo enviado porque no es necesario en el backend
  id:Number(route.query.id)
})

const mostrarFormulario = ref<boolean>(true)
const cargandoFoto = ref<boolean>(false)

function subirFoto():void {
  cargandoFoto.value = true
  let data = new FormData()
  if(imagen.value !== undefined){
    infoFoto.nombreFoto = imagen.value[0].name
    data.append('imagen',imagen.value[0])
    data.append('data',JSON.stringify(infoFoto))
      // console.log("data",data.values())
  }
  axios.post(import.meta.env.VITE_API_SUBIR_FOTO, data)
  .then((res:AxiosResponse)=>{
    // console.log('res',res)
    mostrarFormulario.value = false
    alert.gestionarRespuesta(res)
    setTimeout(() => {
      router.push({name:'Lista de fotos'})
      // mostrarInfoFoto.value = true // muestra el formulario de datos de imagen para guardar en la base de datos
    }, 3000);

  })
  .catch((err:AxiosError)=>{
    // console.log('err',err)
    mostrarFormulario.value = false
    alert.gestionarError(err)
    setTimeout(() => {
      mostrarFormulario.value = true
      cargandoFoto.value = false
    }, 3000);
  })

}


function nuevaFoto():void {
  mostrarFormulario.value = true
  infoFoto.nombreFoto = ''
  infoFoto.direccionUrl = ''
}
</script>

<style scoped>
</style>
