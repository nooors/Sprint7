<template>
  <div>
    <b-row class="mb-2">
      <b-col class="d-flex justify-content-start">
        Ordena els pressupostos
      </b-col>
    </b-row>
    <b-row class="buttons mb-2" size="sm">
      <b-col class="d-flex justify-content-start">
        <b-button class="mr-2" size="sm" @click="sortquote('alpha')"
          >alfabèticament</b-button
        >
        <b-button class="mr-2" size="sm" @click="sortquote('date')"
          >per data</b-button
        >
        <b-button size="sm" @click="sortquote('reset')">reinicia</b-button>
      </b-col>
    </b-row>
    <div class="quotes" v-if="dataQuotes.length > 0">
      <b-list-group class="text-left">
        <div class="list mb-2" v-for="(dataQuote, index) in dataQuotes" :key="index">
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
      type: [],
      required: true,
    },
  },
  filters: {
    formatdata: function (value) {
      return value.toLocaleString();
    },
    formatPrize: function (value) {
      return `${value.toFixed(2)} €`;
    },
  },
  methods: {
    sortquote(value) {
      this.$emit("sortQuote", value);
    },
  },
};
</script>

<style></style>
