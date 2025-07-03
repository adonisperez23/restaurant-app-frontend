<template>
    <v-container style="max-width: 1200px" class="mt-5 pt-5 mb-16 pb-16">
        <v-row class="mt-16 pt-16 mb-16 pb-16">
            <v-col>
                <h3 class="text-left">En nuestra aplicación podras:</h3>
                <v-expansion-panels color="#f3d595">
                    <v-expansion-panel
                        bg-color="#fcecd2"
                        variant="Popout"
                        title="Ver el menú"
                        text="Visualiza nuestro menú disponible, donde podrás ver todos los detalles de cada plato: su precio y cómo está elaborado.
          "
                    ></v-expansion-panel>
                    <v-expansion-panel
                        bg-color="#fcecd2"
                        variant="Popout"
                        title="Registrarte en la aplicación"
                        text="Podrás registrarte fácil y rápidamente en nuestra aplicación ingresando tu nombre, correo electrónico y número de teléfono.
          "
                    ></v-expansion-panel>
                    <v-expansion-panel
                        bg-color="#fcecd2"
                        variant="Popout"
                        title="Seleccionar plato y contornos"
                        text="En la aplicación observará un boton en cada plato con la palabra 'PEDIR'.
          Al darle click, se desplegará una ventana donde podrá visualizar todos los contornos disponibles y que posteriormente
          podrá elegir hasta 3 contornos de todos los que se encuentren disponibles para que complementen su plato. Al tener su plato y sus contornos
          seleccionados le podrá dar al boton 'AGREGAR A LA LISTA' para que su plato sea agregado a la lista de pedidos.
          "
                    ></v-expansion-panel>
                    <v-expansion-panel
                        bg-color="#fcecd2"
                        variant="Popout"
                        title="Ver pedido"
                        text="En la barra navegadora de la aplicación, podrá observar una pestaña que dice 'Lista de pedidos(0)' que indica la cantidad
          de productos que usted habra agregado. Al darle click, podrá visualizar todos sus productos. Además visualizará las cantidades, precio de cada plato, sus montos por cada plato y el monto final
          del pedido. Con el monto final observará un boton llamado 'Enviar pedido'.
          "
                    ></v-expansion-panel>
                    <v-expansion-panel
                        bg-color="#fcecd2"
                        variant="Popout"
                        title="Enviar pedido"
                        text="De forma detallada, el boton 'ENVIAR PEDIDO' abrirá su aplicación de whatsapp con un mensaje de texto
          prederterminado con los detalles del pedido que previamente habrá armado en la aplicación y se enviará al numero de whatsapp del encargado que le respondera el mensaje para confirmar detalles del pedido."
                    ></v-expansion-panel>
                </v-expansion-panels>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup lang="ts"></script>

<style></style>
