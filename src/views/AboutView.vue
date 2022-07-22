<script>
export default {
  data() {
    return {
      elementos: [],
      inicio: 1,
      fin: 51,
    };
  },
  mounted() {
    this.elementos = this.consulta(this.inicio, this.fin);
  },
  methods: {
    selectCard(item) {
      //
      console.log(item.nombre);
    },

    consulta(inicio, fin) {
      let datos = [];
      const myPromise = new Promise((resolve, reject) => {
        for (let index = inicio; index < fin; index++) {
          fetch(`https://pokeapi.co/api/v2/pokemon/${index}/`)
            .then((response) => response.json())
            .then((data) => {
              datos.push({
                titulo: "Titulo",
                nombre: data.name,
                id: data.id,
                color: "rojo",
                colorAcent: "rojoTipo",
                colorNumero: "rojoNumero",
                numero:
                  "#" + data.id.toString().length < 3
                    ? PadLeft("0" + data.id, length)
                    : data.id,
              });
            });
        }

        setTimeout(() => {
          datos.sort(function (a, b) {
            if (a.id > b.id) {
              return 1;
            }
            if (a.id < b.id) {
              return -1;
            }
            // a must be equal to b
            return 0;
          });
          resolve(datos);
        }, 300);
      });

      myPromise.then((datos) => {
        this.elementos = datos;
      });
    },

    siguientes() {
      //console.log(this.inicio);
      if (this.inicio >= 851) {
        this.inicio = 901;
        this.fin = 906;
        this.consulta(this.inicio, this.fin);
      } else {
        this.inicio = this.inicio + 50;
        this.fin += 50;

        this.consulta(this.inicio, this.fin);
      }
    },

    anteriores() {
      if (this.inicio == 1) {
        //console.log("Ya es todo no existe el -1 :v");
      } else {
        if (this.inicio == 901) {
          this.inicio = this.inicio - 50;
          this.fin = 901;

          this.consulta(this.inicio, this.fin);
        } else {
          this.inicio = this.inicio - 50;
          this.fin -= 50;

          this.consulta(this.inicio, this.fin);
        }
      }
    },
  },
};
</script>

<template>
  <div class="about">
    <h1>Cards</h1>

    <div style="display: flex">
      <div @click="anteriores" class="botonPlano">Anteriores</div>
      <div @click="siguientes" class="botonPlano">Siguientes</div>
    </div>

    <div class="contenedor">
      <div
        class="card"
        :class="[item.color]"
        v-for="item in elementos"
        :key="item.id"
        @click="selectCard(item)"
      >
        <span class="numero" :class="[item.colorNumero]">
          {{ item.numero }}
        </span>
        <span class="titulo"> {{ item.titulo }} </span>
        <span class="color" :class="[item.colorAcent]"> {{ item.color }} </span>
      </div>
    </div>
  </div>
</template>

<style>
.botonPlano {
  display: flex;
  justify-content: center;
  max-width: 8rem;
  margin: 1rem;
  padding: 1rem;
  background-color: royalblue;
  transition: box-shadow 0.3s;
}

.botonPlano:hover {
  cursor: pointer;
}

.botonPlano:active {
  box-shadow: 5px 5px 10px blueviolet, -5px -5px 10px blueviolet;
}

.contenedor {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 18rem;
  height: 8rem;
  border-radius: 1rem;
  padding: 0.5rem;
  margin: 0.5rem;
  transition: box-shadow 0.3s;
}

.numero {
  display: flex;
  justify-content: end;
  font-family: "Roboto-Black";
}

.titulo {
  display: flex;
  justify-content: start;
  font-family: "Roboto-Regular";
  font-size: 1.5rem;
}

.color {
  padding: 0.2rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  margin-top: 0.2rem;
  border-radius: 1rem;
}
</style>
