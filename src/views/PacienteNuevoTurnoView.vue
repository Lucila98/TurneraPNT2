<script setup>
import { ref } from 'vue'
import { storeToRefs } from 'pinia'
import { useUserStore } from '../stores/user'
import { useMedicosStore } from '../stores/medicos'
import { useRouter } from "vue-router";
const medicos = useMedicosStore()
const router = useRouter();
const selectorEspecialidad = ref("")
let medicosFiltrados = ref([])

const revelarMedicos = () => {
  console.log("valor del selector", selectorEspecialidad.value);
  switch (selectorEspecialidad.value) {
    case "1":
      medicosFiltrados.value = medicos.pediatras
      break;
    case "2":
      medicosFiltrados.value = medicos.clinicos
      break;
    case "3":
      medicosFiltrados.value = medicos.urologos
      break;
  }
  console.log(medicosFiltrados);
}

const reservado = () => { 
  alert("Reservado!") 
  router.push("/exitoNuevoTurno")
}

let horarios = ref([
  {
    hora: "10:00",
    disponible: true
  },
  {
    hora: "11:00",
    disponible: false
  },
  {
    hora: "12:00",
    disponible: false
  },
  {
    hora: "13:00",
    disponible: true
  },
  {
    hora: "14:00",
    disponible: true
  },
  {
    hora: "15:00",
    disponible: true
  }
])

</script>

<template>
  <main>
    <div class="formulario text-center">
      <h1>Nuevo Turno</h1>
      <select v-model="selectorEspecialidad" v-on:change="revelarMedicos" class="form-select">
        <option value="1">Pediatría</option>
        <option value="2">Clínico</option>
        <option value="3">Urólogo</option>
      </select>
      <select class="form-select">
        <option value="#" selected disabled>Seleccione un médico</option>
        <option v-for="medico in medicosFiltrados" value="medico.nombre">{{ medico.nombre }}</option>
      </select>
      <input type="date" class="form-control"> <br>
      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Hora</th>
            <th scope="col">Disponible</th>
            <th scope="col">Reservar</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="hora in horarios">
            <th scope="row">{{ hora.hora }}</th>
            <td v-if="hora.disponible">Si</td>
            <td v-if="!hora.disponible">No</td>
            <td v-if="hora.disponible"><button @click="reservado" class="btn btn-success">Reservar</button></td>
            <td v-if="!hora.disponible"><button class="btn btn-danger" disabled>No disponible</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<style>
.formulario {
  display: flex;
  flex-flow: column nowrap;
  align-content: space-between;
  height: 100vw;
}

main {
  height: 43vw;
}
</style>