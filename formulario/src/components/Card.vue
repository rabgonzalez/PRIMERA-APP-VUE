<template>
  <div class="card carta">
    <div class="card-body">
      <h3 class="card-title">{{ personaje.nombre }}</h3>
      <div class="card-text text-start">
        <ul class="list-group list-group-flush">
          <li class="list-group-item ms-3 crear">
            <b class="bold">Origen:</b> {{ personaje.origen }}
          </li>
          <li class="list-group-item ms-3 crear">
            <b class="bold">Habilidad:</b> {{ personaje.habilidad }}
          </li>
          <li class="list-group-item ms-3 crear">
            <b class="bold">Aliados:</b>
            {{
              personaje.aliados.length > 0
                ? personaje.aliados.join(",")
                : "ninguno"
            }}
          </li>
          <li class="list-group-item ms-3 crear">
            <b class="bold">Mision cumplida:</b>
            {{ personaje.mision ? "Si" : "No" }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: string[];
  mision: boolean;
};

export default defineComponent({
  props: {
    personaje: {
      type: Object as () => Personaje,
      required: true,
    },
  },
  setup(props) {
    console.log("Personaje recibido:", props.personaje); // Verifica el contenido
  },
});
</script>

<style lang="css" scoped>
.carta {
  background-color: #eeeeee;
  box-shadow: 2px 2px 0 2px #d1a349;
}

.bold {
  color: #d4af37;
}
</style>
