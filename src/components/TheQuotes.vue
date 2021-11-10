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
    <!-- Renderitzat dels pressupostos -->
    <div class="quotes">
      <b-list-group class="text-left">
        <div
          class="list mb-2"
          v-for="dataQuote in dataQuotes"
          :key="dataQuote.id"
        >
          <b-list-group-item
            >Pressupost: {{ dataQuote.quote }}</b-list-group-item
          >
          <b-list-group-item>Usuari: {{ dataQuote.user }}</b-list-group-item>
          <b-list-group-item
            >Serveis contractats:
            <b-list-group>
              <div
                class="list__services"
                v-for="(serviceQuote, index) in dataQuote.choose"
                :key="index"
              >
                <b-list-group-item>{{ serviceQuote }}</b-list-group-item>
              </div>
            </b-list-group>
          </b-list-group-item>
          <b-list-group-item
            >Preu: {{ dataQuote.total | formatPrize }}</b-list-group-item
          >
          <b-list-group-item
            >Data: {{ dataQuote.date | formatdata }}</b-list-group-item
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
    };
  },
  methods: {
    sortQuotes: function (value) {
      switch (value) {
        case "alpha":
          this.dataQuotes = this.dataQuotes.sort(function (a, b) {
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
          return this.dataQuotes;
          break;
        case "price":
          this.dataQuotes = this.dataQuotes.sort(function (a, b) {
            return a.total - b.total;
          });
          return this.dataQuotes;
          break;
        case "reset":
          this.dataQuotes = this.copyDataQuotes;
          return this.dataQuotes;
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
  computed: {
    copyData: function () {
      if (this.copyDataQuotes.length < this.dataQuotes.length) {
        this.copyDataQuotes.push(this.dataQuotes[this.dataQuotes.length - 1]);
      }
      // return this.copyDataQuotes;
    },
  },
  filters: {
    formatdata: function (value) {
      return value.toLocaleString(); // Date output format
    },
    formatPrize: function (value) {
      return `${value.toFixed(2)} €`; // Amount output format
    },
  },
};
</script>

<style></style>
