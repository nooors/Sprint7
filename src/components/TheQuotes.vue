<template>
  <div v-if="dataQuotes.length">
    <b-row class="mb-2">
      <b-col class="d-flex justify-content-start">
        Ordena els pressupostos
        <!-- Botons per ordenar els pressupostos -->
      </b-col>
    </b-row>
    <b-row class="buttons mb-2" size="sm">
      <b-col class="d-flex justify-content-start">
        <b-button class="mr-2" size="sm" @click="sortQuotes('alpha')"
          >alfabèticament</b-button
        >
        <b-button class="mr-2" size="sm" @click="sortQuotes('price')"
          >pel total</b-button
        >
        <b-button size="sm" @click="sortQuotes('reset')">reinicia</b-button>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
         <b-input-group size="sm" class="mb-2">
          <b-input-group-prepend is-text>
            <b-icon icon="search"></b-icon>
          </b-input-group-prepend>
          <b-form-input type="search" placeholder="Busca pel nom del pressupost" v-model="query"></b-form-input>
        </b-input-group>
      </b-col>
    </b-row>
    <!-- renderitzat de la recerca -->
    <!-- <div v-if="query"> -->
      <!-- Si hi ha una recerca pinto la recerca -->
    <!-- </div> -->
    <!-- Renderitzat dels pressupostos -->
    <div class="quotes">
      <!-- Si no hi ha búsqueda pinto el llistat de pressupostos -->
      <b-list-group class="text-left">
        <div
          class="list mb-2"
          v-for="copyDataQuote in copyDataQuotes"
          :key="copyDataQuote.id"
        >
          <b-list-group-item
            >Pressupost: {{ copyDataQuote.quote }}</b-list-group-item
          >
          <b-list-group-item
            >Usuari: {{ copyDataQuote.user }}</b-list-group-item
          >
          <b-list-group-item
            >Serveis contractats:
            <b-list-group>
              <div
                class="list__services"
                v-for="(serviceQuote, index) in copyDataQuote.choose"
                :key="index"
              >
                <b-list-group-item>{{ serviceQuote }}</b-list-group-item>
              </div>
            </b-list-group>
          </b-list-group-item>
          <b-list-group-item
            >Preu: {{ copyDataQuote.total | formatPrize }}</b-list-group-item
          >
          <b-list-group-item
            >Data: {{ copyDataQuote.date | formatdata }}</b-list-group-item
          >
        </div>
      </b-list-group>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheQuotes",
  props: {
    dataQuotes: Array,
  },
  data() {
    return {
      copyDataQuotes: [],
      query: "",
    };
  },
  computed: {
    copyData: function () {
      if (this.copyDataQuotes.length < this.dataQuotes.length) {
        this.copyDataQuotes.push(this.dataQuotes[this.dataQuotes.length - 1]);
      }
      // return this.copyDataQuotes;
    },
    // searched: function(){
    //   if(!this.query) return this.copyDataQuotes = this.dataQuotes.slice();
    //   return this.copyDataQuotes = this.copyDataQuotes.filter(name => {
    //     return name.quote.includes(this.query)})
    // },
  },
  filters: {
    formatdata: function (value) {
      return value.toLocaleString(); // Date output format
    },
    formatPrize: function (value) {
      return `${value.toFixed(2)} €`; // Amount output format
    },
  },
  methods: {
    sortQuotes: function (value) {
      switch (value) {
        case "alpha":
          this.copyDataQuotes = this.copyDataQuotes.sort(function (a, b) {
            let nameA = a.quote.toLowerCase();
            let nameB = b.quote.toLowerCase();
            if (nameA < nameB) {
              return -1;
            }
            if (nameA > nameB) {
              return 1;
            }
            return 0;
          });
          return this.copyDataQuotes;
          break;
        case "price":
          this.copyDataQuotes = this.copyDataQuotes.sort(function (a, b) {
            return a.total - b.total;
          });
          return this.copyDataQuotes;
          break;
        case "reset":
          this.copyDataQuotes = this.dataQuotes.slice();
          return this.copyDataQuotes;
      }
    },
  },
  // watch: {
  //   dataQuotes: function() {
  //     console.log("WATCHED");
  //     console.log(dataQuotes);
  //     if (this.dataQuotes.length) {
  //        return this.copyDataQuotes = this.dataQuotes.slice();
  //     }
  //   },
  // },
};
</script>

<style></style>
