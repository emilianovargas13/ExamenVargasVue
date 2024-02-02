<template>
  <div>

    <div class="m-5">
      <b-breadcrumb :items="items"></b-breadcrumb>
    </div>

    <div class="m-5">

      <b-form @submit="onSubmit" v-if="show" >
        <b-row>
          <b-col>
            
            <b-form-group id="marca" label="Marca" placeholder="">

              <b-form-input
                placeholder="Ejemplo: Nissan"
                id="marca"
                v-model="form.marca"
                type="text"
                required
                pattern="[A-Za-z0-9]+">


              </b-form-input> </b-form-group>

            </b-col>
          <b-col>

            <b-form-group id="modelo" label="Modelo">
              <b-form-input
              placeholder="Ejemplo: Versa"
                id="modelo"
                v-model="form.modelo"
                type="text"
                pattern="[A-Za-z0-9]+"
                required>
              
              </b-form-input> 
            </b-form-group>
            </b-col>

          <b-col>
            <b-form-group id="anio" label="Año">
              <b-form-input
                placeholder="Ejemplo: 2024"
                id="anio"
                v-model="form.anio"
                type="number"
                required>
              
              </b-form-input> 
            </b-form-group>
            </b-col>

        </b-row>
        <b-row>

          <b-col>
            <b-form-group id="numero_serie" label=" Numero de serie">
              <b-form-input
                placeholder="Ejemplo: XXXX000-00XX "
                id="numero_serie"
                v-model="form.numero_serie"
                type="text"
                required>

              </b-form-input> 
              </b-form-group>
            </b-col>
            
        </b-row>
<p>

</p>
        <b-button type="submit" class="float-right" style="background-color: green;">Registrar</b-button>
       
      </b-form>

      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ form }}</pre>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {

  data() {


    return {
      show: true,
      form: {
        marca: "",
        modelo: "",
        anio: "",
        numero_serie: "",
      },


      items: [
        {
          text: "Inicio",
          to: "/",
        },
        {
          text: "Formulario",
          active: true,
        },
        {
          text: "Paginacion",
          to: "/paginacion",
        },
      ],
    };
  },
  
  methods: {
    onSubmit(event) {
      event.preventDefault();
      const year = new Date().getFullYear();



      if (this.form.anio > year) {
        alert("El año es mayor que el actual, ERROR 400.");
        return false; 
      }
      const regex = /^[A-Za-z]{4}\d{3}-\d{2}[A-Za-z]{2}$/;
      if (!regex.test(this.form.numero_serie)) {
        alert("El número de serie es incorrecto, deben ser 11 digitos entre letras y numeros");
        return;
      }



      const formData = {
        brand: this.form.marca,
        model: this.form.modelo,
        year: this.form.anio,
        serie: this.form.numero_serie,
      };
      fetch("http://localhost:8080/api/vehiculos", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(formData),
      })
        .then((response) => {
          if (!response.ok) {
            throw new Error("Error en el servidor");
          }
          alert("Registro Realizado")
          return response.json();
        })
        .catch((error) => {
          console.error("Error:", error);
          alert("Error en la solicitud/servidor");
        });
    },
  },
};
</script>

<style></style>
