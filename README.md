# PRIMERA-APP-VUE
# Ruben Abreu Gonzalez

## Índice
- [PRIMERA-APP-VUE](#primera-app-vue)
- [Ruben Abreu Gonzalez](#ruben-abreu-gonzalez)
  - [Índice](#índice)
  - [Pasos](#pasos)
    - [Instalación](#instalación)
    - [Definición](#definición)
      - [Script](#script)
      - [Template](#template)

## Pasos
### Instalación
Para crear el proyecto con Vue, primero descargaremos los paquetes de Vue.
> npm install -g @vue/cli

Una vez instalada la biblioteca, para crear el proyecto ejecutamos el siguiente comando:
> vue create formulario

Y seleccionamos Vue-3 con NPM, nos debería de dar una salida así
```bash
alumno@alumno-aed:~/rabgonzalez/PRIMERA-APP-VUE$ vue create formulario
00h00m00s 0/0: : 

Vue CLI v5.0.8
Failed to check for updates
? Please pick a preset: Default ([Vue 3] babel, eslint)
? Pick the package manager to use when installing dependencies: NPM


Vue CLI v5.0.8
Failed to check for updates
✨  Creating project in /home/alumno/rabgonzalez/PRIMERA-APP-VUE/formulario.
⚙️  Installing CLI plugins. This might take a while...


added 821 packages, and audited 822 packages in 28s

100 packages are looking for funding
  run `npm fund` for details

8 vulnerabilities (4 moderate, 4 high)

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
🚀  Invoking generators...
📦  Installing additional dependencies...


added 88 packages, and audited 910 packages in 5s

112 packages are looking for funding
  run `npm fund` for details

8 vulnerabilities (4 moderate, 4 high)

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
⚓  Running completion hooks...

📄  Generating README.md...

🎉  Successfully created project formulario.
👉  Get started with the following commands:

 $ cd formulario
 $ npm run serve
```

### Definición
#### Script
Dentro del script es dónde encontraremos toda la parte lógica del programa, vemos que en la primera línea importamos las librerías de vue que más tarde utilizaremos y creamos un objeto llamado personaje que definde la estructura de objetos que aceptará nuestro programa.
```typeScript
type Personaje = {
  nombre: string;
  origen: string;
  habilidad: string;
  aliados: string[];
  mision: boolean;
}
```

En el setup() creamos 3 variables:
1. **crearPersonaje: boolean;**
2. **personaje: Personaje;**
3. **personajes: Personaje[];**
   
---

1. **crearPersonaje** decide los elementos que se mostrarán en pantalla, si está en false mostrará la lista de los personajes creados y si está en true mostrará el formulario de creación de personajes. 
También le hemos creado un método (setCrearPersonaje) que al llamarlo modificará el valor del boolean.

> [!TIP] Importante
crearPersonaje utiliza la librería ref() ya que queremos que el valor de la variable persista entre renderizados.

2. **personaje** guardar la información del personaje que creamos en el formulario.
El formulario llama a la función agregarPersonaje:
```typescript
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
```

1. **personajes** es una lista de todos los personajes que creamos en el formulario, está es de tipo reactivo porque queremos que la lista cambie cada vez que creamos un nuevo personaje.

#### Template
El template es la parte que se va a visualizar del programa. Está se divide en varios grupos:
1. **boton**
2. **formulario**
3. **lista**
   
---

1. El botón decide cúal de los otros grupos se va a mostrar en pantalla.
Este utiliza 2 directivas de vue:
- **v-if / v-else:** se utiliza para saber qué mensaje mostrar
- **v-on (@click):** al hacer click sobre el botón ejecuta la función "setCrearPersonaje"

2. El formulario utiliza 3 directivas de vue:
- **v-show:** solo se muestra si la condición es cierta
- **v-model:** cada vez que un valor de los input cambie, esté se aplicará en la variable personaje modificando sus valores.
- **v-on (@submit):** cuando se pulse el botón se ejecutará la funcion "agregarPersonaje", utiliza el modificador prevent que evita que la página se renderice al pulsarlo. 

3. La lista es un bucle de cartas de boostrap con la información de cada personaje, utiliza 3 directivas de vue, siendo v-for una de las nuevas:
- **v-for:** se utiliza para realizar un bucle, nosotros la utilizamos para crear una carta por cada personaje que tengamos en la lista, estos bucles requieren de una key para diferenciarlo del resto de elementos.

> [!TIP] Importante
> Al utilizar v-for también estamos haciendo uso de otra directiva, **v-bind**, pero se puede sustituir por los 2 puntos **:**, esta directiva sirve para asociar un atributo de HTML a una variable de JavaScript
> ```typeScript
> <option
>   v-for="aliado in personajes"
>   :key="aliado.nombre"
>   :value="aliado.nombre"
> >
> ```