<template>
  <div v-if="dataQuotes.length">
    <b-row class="mb-2">
      <b-col class="d-flex justify-content-start">
        Ordena els pressupostos
        <!-- Butttons for sort quotes-->
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
    <!-- Search Button -->
    <b-row>
      <b-col>
        <b-input-group size="sm" class="mb-2">
          <b-input-group-prepend is-text>
            <b-icon icon="search"></b-icon>
          </b-input-group-prepend>
          <b-form-input
            type="search"
            placeholder="Busca pel nom del pressupost"
            v-model="query"
          ></b-form-input>
        </b-input-group>
      </b-col>
    </b-row>
    <!-- Quotes render -->
    <div class="quotes">
      <b-list-group class="text-left">
        <div
          class="list mb-2"
          v-for="copyDataItem in copyData"
          :key="copyDataItem.id"
        >
          <b-list-group-item
            >Pressupost: {{ copyDataItem.quote }}</b-list-group-item
          >
          <b-list-group-item>Usuari: {{ copyDataItem.user }}</b-list-group-item>
          <b-list-group-item
            >Serveis contractats:
            <b-list-group>
              <div
                class="list__services"
                v-for="(serviceQuote, index) in copyDataItem.choose"
                :key="index"
              >
                <b-list-group-item>{{ serviceQuote }}</b-list-group-item>
              </div>
            </b-list-group>
          </b-list-group-item>
          <b-list-group-item
            >Preu: {{ copyDataItem.total | formatPrize }}</b-list-group-item
          >
          <b-list-group-item
            >Data: {{ copyDataItem.date | formatdata }}</b-list-group-item
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
      filterSort: "",
    };
  },
  computed: {
    copyData: function () {
      this.copyDataQuotes = this.dataQuotes.slice();
      if (this.query) {
        return this.copyDataQuotes.filter((name) => {
          return name.quote.includes(this.query);
        });
      }
      if (this.filterSort) {
        switch (this.filterSort) {
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
      }
      return this.copyDataQuotes;
    },
    searched: function () {
      if (this.query && this.copyDataQuotes.length == this.dataQuotes.length) {
        this.copyDataQuotes = this.dataQuotes.slice();
        return (this.copyDataQuotes = this.copyDataQuotes.filter((name) => {
          return name.quote.includes(this.query);
        }));
      }
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
  methods: {
    sortQuotes: function (value) {
      this.filterSort = value;
      console.log(this.filterSort);
    },
  },
};
</script>

<style></style>
