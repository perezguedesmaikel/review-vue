<script setup>
import {useRouter} from "vue-router";

const items = [
  {title: 'My Home', redirect: '/'},
  {title: 'My counter', redirect: '/counter'},
  {title: 'Tablero Canvas', redirect: '/tablero'},
  {title: 'Form', redirect: '/form'},
  {title: 'Click Me 2', redirect: '/counter'},
]
const router = useRouter();
const navigateTo = (route) => {
  router.push(route);
};
</script>
<template>
  <div class="d-flex justify-space-around">
    <v-menu>
      <template v-slot:activator="{ props }">
        <v-app-bar-nav-icon v-bind="props"/>
      </template>
      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
          :value="index"
          @click="navigateTo(item.redirect)"
        >
          {{ item.title }}

        </v-list-item>
      </v-list>
    </v-menu>
  </div>
</template>
<style scoped>


</style>
