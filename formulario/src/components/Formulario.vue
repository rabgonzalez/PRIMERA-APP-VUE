<template>
  <button
    class="btn btn-warning"
    @click="setCrearPersonaje"
    v-if="crearPersonaje"
  >
    Volver a la lista
  </button>
  <button class="btn btn-primary" @click="setCrearPersonaje" v-else>
    Crear Personaje
  </button>

  <div class="container">
    <form
      class="form mt-3 text-start border rounded-3 p-5 bg-muted"
      v-show="crearPersonaje"
      @submit.prevent="agregarPersonaje"
    >
      <div class="mb-3">
        <label for="nombre" class="form-label">Nombre</label>
        <input
          type="text"
          class="form-control"
          v-model="personaje.nombre"
          id="nombre"
          required
        />
      </div>
      <div class="mb-3">
        <label for="origen" class="form-label">Origen</label>
        <input
          type="text"
          class="form-control"
          v-model="personaje.origen"
          id="origen"
          required
        />
      </div>
      <div class="mb-3">
        <label for="habilidad" class="form-label">Habilidad</label>
        <input
          type="text"
          class="form-control"
          v-model="personaje.habilidad"
          id="habilidad"
          required
        />
      </div>
      <div class="aliados" v-show="personajes.length > 0">
        <label for="select" class="form-title">Aliados</label>
        <select
          id="select"
          class="form-control"
          v-model="personaje.aliados"
          multiple
        >
          <option
            v-for="aliado in personajes"
            :key="aliado.nombre"
            :value="aliado.nombre"
          >
            {{ aliado.nombre }}
          </option>
        </select>
      </div>
      <div class="mb-3 mt-3 form-check">
        <input
          type="checkbox"
          class="form-check-input"
          id="mision"
          v-model="personaje.mision"
        />
        <label class="form-check-label" for="mision">Misión cumplida</label>
      </div>
      <button class="btn btn-primary mb-3">Agregar Personaje</button>
    </form>
  </div>

  <div class="container">
    <div class="row">
      <div
        class="col-12 col-md-4 mt-3"
        v-show="crearPersonaje === false"
        v-for="personaje in personajes"
        :key="personaje.nombre"
      >
        <div class="card">
          <div class="card-body">
            <h3 class="card-title">{{ personaje.nombre }}</h3>
            <div class="card-text text-start">
              <ul class="list-group list-group-flush">
                <li class="list-group-item">
                  <b>Origen:</b> {{ personaje.origen }}
                </li>
                <li class="list-group-item">
                  <b>Habilidad:</b> {{ personaje.habilidad }}
                </li>
                <li class="list-group-item">
                  <b>Aliados:</b>
                  {{
                    personaje.aliados.length > 0
                      ? personaje.aliados.join(",")
                      : "ninguno"
                  }}
                </li>
                <li class="list-group-item">
                  <b>Mision cumplida:</b> {{ personaje.mision ? "Si" : "No" }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";

type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: Personaje[];
  mision: boolean;
};

export default defineComponent({
  setup() {
    let crearPersonaje = ref(false);
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
      //Hace una copia de la variable personaje
      let newPersonaje: Personaje = JSON.parse(JSON.stringify(personaje));
      personajes.push(newPersonaje);

      //Limpia el formulario
      personaje.nombre = "";
      personaje.origen = "";
      personaje.habilidad = "";
      personaje.aliados = [];
      personaje.mision = false;

      //Oculta el formulario y muestra la lista de personajes
      crearPersonaje.value = false;
    };

    const setCrearPersonaje = () => {
      crearPersonaje.value = !crearPersonaje.value;
    };

    return {
      personajes,
      personaje,
      agregarPersonaje,
      crearPersonaje,
      setCrearPersonaje,
    };
  },
});
</script>

<style lang="css" scoped></style>
