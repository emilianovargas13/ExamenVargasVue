<template>

  <div>

    <div class="m-5">

      <b-breadcrumb :items="items"></b-breadcrumb>

    </div>

    <div class="overflow-auto">
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="my-table">

      </b-pagination>

      <p class="mt-3">Current Page: {{ currentPage }}</p>

      <b-table
        id="my-table"
        :items="itemsW"
        :per-page="perPage"
        :current-page="currentPage"
        small
        :fields="fields"
        :sort-by.sync="sortBy"
        :sort-desc.sync="sortDesc"
        label-sort-asc=""
        label-sort-desc=""
        :filter="filtro"
        @filtered="onFiltered"

      ></b-table>
    </div>
  </div>
</template>

<script>

export default {


  data() {

    return {

      perPage: 2,
      currentPage: 0,
      itemsW: [],
      filtro: null,
      sortBy: "name",
      sortDesc: false,
      fields: [
        { key: "id", label: "ID", sortable: true },
        { key: "brand", label: "Marca", sortable: true },
        { key: "model", label: "Modelo", sortable: true },
        { key: "year", label: "Año", sortable: true },
        { key: "serie", label: "Numero de serie", sortable: true },
      ],

      items: [
        {
          text: "Inicio",
          to: "/",
        },
        {
          text: "Formulario",
          to: "/formulario",
        },
        {
          text: "Paginacion",
          active: true,
        },
      ],
    };
  },

  methods: {

    fetchData() {
      fetch("http://localhost:8080/api/vehiculos/page", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
          if (!response.ok) {
            throw new Error("Error en la solicitud/servidor");
          }
          return response.json();
        })
        .then((data) => {
          this.itemsW = data.content;
        })
        .catch((error) => {
          console.error("Error al mostrar datos", error);
        });
    },
    onFiltered(filteredItems) {
      this.currentPage = 1;
      this.rows = filteredItems.length;
    },
  },


  mounted() {
    this.fetchData();
  },

  created() {
    this.fetchData();
  },


  computed: {
    rows() {
      return this.itemsW.length;
    },
  },
};
</script>

<style>
</style>

