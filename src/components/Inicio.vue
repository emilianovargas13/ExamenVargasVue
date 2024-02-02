<template>
  <div>

    


    <template>
      <div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">NavBar</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item >

          <b-breadcrumb :items="items"></b-breadcrumb>
        </b-nav-item>
        

        <div>
      
    </div>


      </b-navbar-nav>

      
      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
        </b-nav-form>

       

        
          
          <template #button-content>
           

            
          </template>
        
        
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>

<h3>Estás en el sitio principal mi querido amigo</h3>
    <img src="perrito.jpg" alt="Descripción de la imagen" style="width: 300px; height: auto;" />


    
  </div>

  
</template>

<script>
export default {

  data() {
    
    return {
      items: [
        {
          text: "Inicio",
          active: true,
        },
        {
          text: "Formulario",
          to: "/formulario",
        },
        {
          text: "Paginacion",
          to: "/paginacion",
        },
      ],
    };
  },
};
</script>

<style>
</style>