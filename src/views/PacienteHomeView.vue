<script setup>
import { ref } from 'vue'
import { useUserStore } from '../stores/user'
import { useRouter, RouterLink } from "vue-router";
const user = useUserStore()
const router = useRouter();
</script>

<template>
  <main>
    <div class="text-center">
      <h1>Bienvenido, {{ user.nombreUsuario }} {{ user.apellidoUsuario }}</h1>
      <RouterLink to="/pacienteNuevoTurno"><button class="btn btn-primary m-1">Sacar un Turno</button></RouterLink>
      <RouterLink to="/listadoTurnos"><button class="btn btn-primary m-1">Ver mis Turnos</button></RouterLink>
    </div>

  </main>
</template>

