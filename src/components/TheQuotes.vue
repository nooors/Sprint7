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
        <b-button class="mr-2" size="sm" @click="quotesOrded('alpha')"
          >alfabèticament</b-button
        >
        <b-button class="mr-2" size="sm" @click="quotesOrded('date')"
          >per data</b-button
        >
        <b-button size="sm" @click="sortquote('reset')">reinicia</b-button>
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
    dataQuotes: {
      // Recives the array of objects with all the quotes
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      quoteSorted: [],
    };
  },
  filters: {
    formatdata: function (value) {
      return value.toLocaleString(); // Date output format
    },
    formatPrize: function (value) {
      return `${value.toFixed(2)} €`; // Amount output format
    },
  },
  computed: {
    quotesOrded: () => {
      // switch (modif) {
      //   case "reset":
      //     return this.dataQuotes;
      //     break;
      //   case "alpha":
      //     return this.dataQuotes.sort((a, b) => {
      //       let nameA = a.name.toUpperCase();
      //       let nameB = b.name.toUpperCase();
      //       if(nameA < nameB){
      //         return -1;
      //       }
      //       if(nameB > nameB){
      //         return 1
      //       }
      //       return 0;
      //       });
      //     break;
      //   case "date":
      //     return this.dataQuotes.sort((a,b) => {
      //       return a.date - b.date;
      //     });
      //     break;
      //   default:
          return this.dataQuotes;
      // }  
    
    },
  },
  methods: {
    sortquote(value) {
      switch (value) {
        case "quote":
          return this.dataQuotes.sort(a);
          break;
        case "date":
          return this.dataQuotes.sort((a, b) => a.date - b.date);
          break;
        case "reset":
          return this.dataQuotes;
      }
      this.$emit("sortQuote", value);
    },
  },
};
</script>

<style></style>
