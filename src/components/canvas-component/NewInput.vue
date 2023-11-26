<script lang="ts" setup>
import {ref} from "vue";

const text = ref('')

const emits = defineEmits(['onNewItems'])

function handleSubmit() {
  if (text.value !== '') {
    emits('onNewItems', text)
  }
  text.value = ''
}
</script>

<template>
  <v-form @submit.prevent="handleSubmit">
    <v-text-field v-model="text">

    </v-text-field>
  </v-form>
</template>

<style scoped>

</style>
