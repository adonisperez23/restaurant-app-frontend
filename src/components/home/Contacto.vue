<template>
    <v-container class="mt-16 pt-16 text-left">
      <h2 class="px-5">Contactos:</h2>
      <v-row>
        <v-col >
          <div>
            <br>
            <v-icon>mdi-whatsapp</v-icon>
            <p>
              Escribenos a nuestro numero de Whatsapp
              <a href="https://api.whatsapp.com/send?phone=584129797775" target="_blank">+584129797775</a>
            </p>
            <br>
            <v-icon>mdi-instagram</v-icon>
            <p>
              Visita nuestra cuenta de
              <a href="https://www.instagram.com/rest_loscincosabores/" target="_blank">Instagram</a>.
            </p>
            <br>
          </div>
        </v-col>
      </v-row>
    </v-container>
</template>

<script setup lang="ts">

</script>

<style scoped>
  h2{
    background-color: #f3d595;
    display: inline;
    border-radius: 5px;
  }
  p{
    display: inline;
  }
</style>
