<script lang="ts" setup>
import {ref} from "vue";

const counter = ref(0)

function changeCounter(valor: number) {
  counter.value = counter.value + valor
}
</script>

<template>
  <v-container class="MyCounterContainer">
    <v-label>{{ counter }}</v-label>
    <v-btn class="myButtonStyle" color="blue" variant="tonal" @click="()=>changeCounter(1)">
      Incrementar
    </v-btn>
    <v-btn class="myButtonStyle" color="blue" variant="tonal" @click="()=>changeCounter(-1)">
      Decrementar
    </v-btn>
  </v-container>


</template>

<style scoped>
.MyCounterContainer {
  padding: 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.myButtonStyle {
  width: 150px;
  margin: 5px;
}
</style>
