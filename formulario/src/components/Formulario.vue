<template>
  <div class="formulario">
    <button
      class="btn btn-warning mt-5"
      @click="setCrearPersonaje"
      v-if="crearPersonaje"
    >
      Volver a la lista
    </button>
    <button class="btn btn-primary mt-5" @click="setCrearPersonaje" v-else>
      Crear Personaje
    </button>

    <div class="container">
      <form
        class="form mt-3 mb-5 text-start border rounded-3 p-5 crear"
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
      <div class="row" v-if="personajes.length">
        <Card
          class="col-12 col-md-4 mt-3 carta"
          v-show="crearPersonaje === false"
          v-for="personaje in personajes"
          :key="personaje.nombre"
          :personaje="personaje"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import Card from "./Card.vue";
import CardInfo from "./CardInfo.vue";

type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: string[];
  mision: boolean;
};

export default defineComponent({
  components: {
    Card,
    CardInfo,
  },
  setup() {
    let crearPersonaje = ref(false);
    const personajes: Personaje[] = reactive([
      {
        nombre: "Jinx",
        origen: "Zaun",
        habilidad: "Combate a distancia con armas explosivas",
        aliados: ["Silco"],
        mision: false,
      },
      {
        nombre: "Vi",
        origen: "Zaun",
        habilidad: "Combate cuerpo a cuerpo",
        aliados: ["Caitlyn", "Jinx"],
        mision: true,
      },
      {
        nombre: "Caitlyn",
        origen: "Píltover",
        habilidad: "Tiro con precisión",
        aliados: ["Vi"],
        mision: true,
      },
      {
        nombre: "Jayce",
        origen: "Píltover",
        habilidad: "Creación de armas hextech",
        aliados: ["Viktor"],
        mision: true,
      },
      {
        nombre: "Viktor",
        origen: "Zaun",
        habilidad: "Ingeniería avanzada",
        aliados: ["Jayce"],
        mision: true,
      },
      {
        nombre: "Heimerdinger",
        origen: "Píltover",
        habilidad: "Inventor y científico",
        aliados: ["Jayce", "Ekko"],
        mision: false,
      },
      {
        nombre: "Silco",
        origen: "Zaun",
        habilidad: "Liderazgo y manipulación",
        aliados: ["Jinx"],
        mision: false,
      },
      {
        nombre: "Ekko",
        origen: "Zaun",
        habilidad: "Manipulación del tiempo",
        aliados: ["Vi", "Heimerdinger"],
        mision: true,
      },
      {
        nombre: "Mel Medarda",
        origen: "Noxus",
        habilidad: "Diplomacia y estrategia",
        aliados: ["Jayce"],
        mision: true,
      },
      {
        nombre: "Sevika",
        origen: "Zaun",
        habilidad: "Combate cuerpo a cuerpo con brazo mecánico",
        aliados: ["Silco"],
        mision: false,
      },
      {
        nombre: "Marcus",
        origen: "Píltover",
        habilidad: "Corrupción política",
        aliados: [],
        mision: false,
      },
      {
        nombre: "Grayson",
        origen: "Píltover",
        habilidad: "Liderazgo policial",
        aliados: ["Caitlyn"],
        mision: true,
      },
      {
        nombre: "Vander",
        origen: "Zaun",
        habilidad: "Protector y estratega",
        aliados: ["Vi", "Jinx"],
        mision: true,
      },
      {
        nombre: "Mylo",
        origen: "Zaun",
        habilidad: "Espionaje",
        aliados: ["Vi", "Claggor"],
        mision: true,
      },
      {
        nombre: "Claggor",
        origen: "Zaun",
        habilidad: "Fuerza física",
        aliados: ["Vi", "Mylo"],
        mision: true,
      },
      {
        nombre: "Singed",
        origen: "Zaun",
        habilidad: "Química avanzada",
        aliados: ["Silco"],
        mision: false,
      },
      {
        nombre: "Ambessa Medarda",
        origen: "Noxus",
        habilidad: "Estrategia militar",
        aliados: ["Mel Medarda"],
        mision: true,
      },
      {
        nombre: "Finn",
        origen: "Zaun",
        habilidad: "Liderazgo criminal",
        aliados: ["Silco"],
        mision: false,
      },
      {
        nombre: "Renata Glasc",
        origen: "Zaun",
        habilidad: "Química persuasiva",
        aliados: [],
        mision: false,
      },
      {
        nombre: "Ryze",
        origen: "Runaterra",
        habilidad: "Magia ancestral",
        aliados: [],
        mision: true,
      },
    ]);
    let personaje: Personaje = {} as Personaje;

    const agregarPersonaje = () => {
      //Hace una copia de la variable personaje
      //Sirve para no modificar el personaje que ya está introducido en la lista
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

<style lang="css" scoped>
.formulario {
  background-color: #274156;
}

.crear {
  background-color: #eeeeee;
}
</style>
