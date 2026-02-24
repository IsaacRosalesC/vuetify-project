<script setup>
import { ref, computed } from 'vue'

const counter = ref(0);

const classCounter = computed(() => {
  if (counter.value === 0) {
    return {
      color: 'text-white',
      texto: '¡Contador en cero bb!',
      type: 'success'
    };
  } else if (counter.value > 0) {
    return {
      color: 'text-green-500',
      texto: '¡Contador positivo bb!',
      type: 'success'
    };
  } else {
    return {
      color: 'text-red-500',
      texto: '¡Contador negativo cñm!',
      type: 'error'
    };
  }
})

const numbersAdd = ref([]);
const numeroDuplicado = ref(false);

function agregar() {

  // const busquedaNumero = numbersAdd.value.find(number => number === counter.value);
  // if (busquedaNumero) {
  //   return;
  // }
  numbersAdd.value.unshift(counter.value);
}

const classAgregar = computed(() => {
  const busquedaNumero = numbersAdd.value.find(number => number === counter.value);

  if (busquedaNumero === 0) {
    numeroDuplicado.value = true;
    return true;
  }

  if (busquedaNumero) {
    numeroDuplicado.value = true;
    return true;
  } else {
    numeroDuplicado.value = false;
    return false;
  }
});
</script>

<template>
  <v-app>
    <v-main>
      <div class="flex h-9/10 items-center justify-center">
        <v-container align="center" justify="center">

          <v-alert class="w-2/6 mb-4 text-start" :text="classCounter.texto" :type="classCounter.type"></v-alert>

          <div
            class="flex flex-col justify-center items-center bg-grey-darken-4 border max-w-4/6 min-h-80 rounded-lg shadow-xl ">

            <h1 :class="classCounter.color">Contador: {{ counter }}</h1>
            <v-container>
              <v-row align="center" justify="center">
                <v-col cols="auto">
                  <v-btn prepend-icon="fas fa-plus" variant="outlined" @click="counter++" size="small">
                    Incrementar
                  </v-btn>
                </v-col>

                <v-col cols="auto">
                  <v-btn prepend-icon="fas fa-minus" variant="outlined" @click="counter--" size="small">
                    Decrementar
                  </v-btn>
                </v-col>

                <v-col cols="auto">
                  <v-btn prepend-icon="fas fa-rotate" variant="outlined" @click="counter = 0" size="small">
                    Reiniciar
                  </v-btn>
                </v-col>
                <v-col cols="auto">
                  <v-btn prepend-icon="fas fa-shopping-cart" variant="outlined" @click="agregar"
                    :disabled="classAgregar" size="small">
                    Agregar
                  </v-btn>
                </v-col>
              </v-row>
              <!-- <p v-if="numeroDuplicado" class="text-red-500">Este numero ya existe</p> -->
              <v-card class="mx-auto p-8" max-width="300">
                <v-list color="green-darken-1" :items="numbersAdd"></v-list>
                <v-list-item v-if="numbersAdd.length === 0">No hay numeros agregados</v-list-item>
              </v-card>


              <!-- <li v-for="number in numbersAdd" :key="number">
                  {{ number }}
                </li> -->
            </v-container>
          </div>

        </v-container>
      </div>

    </v-main>

    <AppFooter />
  </v-app>
</template>
