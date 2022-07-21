<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1,
          titulo: "Titulo",
          color: "verde",
          colorAcent: "verdeTipo",
          colorNumero: "verdeNumero",
          numero: "#001",
        },
        {
          id: 2,
          titulo: "Titulo azul",
          color: "azul",
          colorAcent: "azulTipo",
          colorNumero: "azulNumero",
          numero: "#002",
        },
        {
          id: 3,
          titulo: "Titulo",
          color: "rojo",
          colorAcent: "rojoTipo",
          colorNumero: "rojoNumero",
          numero: "#003",
        },
      ],
    };
  },
  methods: {
    selectCard(item) {
      //
    },
  },
};
</script>

<template>
  <div class="about">
    <h1>Cards</h1>
    <div class="contenedor">
      <div
        class="card"
        :class="[item.color]"
        v-for="item in items"
        :key="item.id"
        @mouseover="selectCard(item)"
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
}

.titulo {
  display: flex;
  justify-content: start;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

.color {
  padding: 0.2rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  margin-top: 0.2rem;
  border-radius: 1rem;
}
</style>
