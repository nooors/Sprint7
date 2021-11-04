<template>
  <b-container>
    <b-row class="mt-5 mb-3">
      <b-col>
        <h1>Benvingut a la app de pressupostos.</h1>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae, enim? Et,
        eveniet, libero beatae a optio unde totam dignissimos explicabo nostrum
        magnam ipsum neque. Obcaecati odit praesentium reiciendis tenetur aut!
      </b-col>
    </b-row>
    <b-row align-h="end" class="mt-5">
      <b-col class="d-flex justify-content-end">
        <router-link to="/home"
          ><b-button>
            Accedir
          </b-button>
        </router-link>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: "Welcome"
};
</script>

<style></style>
