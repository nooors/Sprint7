<template>
  <b-container>
    <b-row my-5 py-3>
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
    <b-row align-h="end">
      <b-col>
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
