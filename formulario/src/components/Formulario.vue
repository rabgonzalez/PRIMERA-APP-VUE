<template>
  <div class="form">
    <form @submit.prevent="agregarPersonaje">
      <input
        type="text"
        v-model="personaje.nombre"
        placeholder="Nombre"
        required
      />
      <input
        type="text"
        v-model="personaje.origen"
        placeholder="Origen"
        required
      />
      <input
        type="text"
        v-model="personaje.habilidad"
        placeholder="Habilidad"
        required
      />
      <div class="aliados" v-show="personajes.length > 0">
        <label for="select">Aliados:</label>
        <select name="select" id="select" v-model="personaje.aliados" multiple>
          <option
            v-for="aliado in personajes"
            :key="aliado.nombre"
            :value="aliado.nombre"
          >
            {{ aliado.nombre }}
          </option>
        </select>
      </div>
      <label for="mision">Misión cumplida:</label>
      <input
        type="checkbox"
        name="mision"
        id="mision"
        v-model="personaje.mision"
      />
      <button type="submit">Agregar Personaje</button>
    </form>
  </div>

  <div
    class="personajes"
    v-for="personaje in personajes"
    :key="personaje.nombre"
  >
    <div class="personaje">
      <h2>{{ personaje.nombre }}</h2>
      <ul>
        <li><b>Origen:</b> {{ personaje.origen }}</li>
        <li><b>Habilidad:</b> {{ personaje.habilidad }}</li>
        <li><b>Aliados:</b> {{ personaje.aliados }}</li>
        <li><b>Mision cumplida:</b> {{ personaje.mision ? "Si" : "No" }}</li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";

type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: Personaje[];
  mision: boolean;
};

export default defineComponent({
  setup() {
    let aliados = 1;
    const personajes: Personaje[] = reactive([
      {
        nombre: "Jinx",
        origen: "Píltover",
        habilidad: "Combate cuerpo a cuerpo",
        aliados: [],
        mision: false,
      },
    ]);
    let personaje: Personaje = {} as Personaje;

    const agregarPersonaje = () => {
      let newPersonaje: Personaje = JSON.parse(JSON.stringify(personaje)); //Hace una copia de la variable personaje
      personajes.push(newPersonaje);
    };

    return {
      personajes,
      personaje,
      agregarPersonaje,
      aliados,
    };
  },
});
</script>

<style lang="css" scoped></style>
