<template>
  <v-form ref="formRef" v-slot="{ valid }" @submit="submitForm">
    <v-container>
      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            v-model="formData.name"
            :rules="nameRules"
            label="Nombre"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-text-field
            v-model="formData.email"
            :rules="emailRules"
            label="Email"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-btn :disabled="!valid" color="primary" type="submit">Enviar</v-btn>
    </v-container>
  </v-form>
</template>

<script setup>
import {ref} from 'vue';


const formData = ref({
  name: '',
  email: ''
});
const formRef = ref(null);

const nameRules = [
  value => !!value || 'El nombre es requerido'
];

const emailRules = [
  value => !!value || 'El email es requerido',
  value => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(value) || 'El email no es válido'
];

const submitForm = () => {
  if (formRef.value.validate()) {
    // Lógica para enviar el formulario
    console.log('Formulario enviado:', formData.value);
  }
};

</script>
