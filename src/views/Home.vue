<template>
  <div class="home">
    <b-row class="text-left mt-3">
      <b-col>
        <h3>Pressupostos App</h3>
        <hr />
      </b-col>
    </b-row>

    <b-row>
      <b-col class="form">
        <b-form @submit="saveQuote">
          <b-form-group v-slot="{ ariaDescribedby }">
            <b-row
              align-h="start"
              v-for="(option, index) in options"
              :key="option.value"
            >
              <b-col class="d-flex justify-content-start">
                <b-form-checkbox
                  v-model="selected"
                  @change="whichIs(index)"
                  :value="index"
                  :aria-describedby="ariaDescribedby"
                  name="flavour-3a"
                >
                  {{ option.text }}
                </b-form-checkbox>
              </b-col>
              <b-row align-h="start" v-show="option.panel">
                <b-col>
                  <transition name="movin">
                    <ThePanel @extrasPanel="dataPanel" />
                  </transition>
                </b-col>
              </b-row>
            </b-row>
          </b-form-group>
          <b-row my-2 class="total">
            <b-col>
              <div class="total_final">Preu: {{ total }}</div>
            </b-col>
          </b-row>
          <b-row class="my-2">
            <b-col class="d-flex justify-content-start">
              Vols guardar el teu pressupost?
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <b-row v-for="(formQuote, index) in formQuotes" :key="index">
                <label for="formQuote">{{ formQuote }}</label>
                <b-form-input
                  type="text"
                  v-model="quoteData[index]"
                ></b-form-input>
              </b-row>
            </b-col>
          </b-row>
          <b-row align-h="end">
            <b-button
              class="my-3"
              type="submit"
              variant="secondary"
              size="sm"
              aria-required="required"
            >
              Guardar pressupost
            </b-button>
          </b-row>
        </b-form>
        <b-row class="text-left">
          <b-col>
            <GoBack />
          </b-col>
        </b-row>
      </b-col>
      <b-col class="quotes">
        <the-quotes :dataQuotes="orderBy" @sortQuote="sortedBy" />
      </b-col>
    </b-row>
  </div>
</template>

<script>
// @ is an alias to /src
import ThePanel from "../components/ThePanel.vue";
import GoBack from "@/components/GoBack.vue";
import TheQuotes from "@/components/TheQuotes.vue";

export default {
  name: "Home",
  components: {
    ThePanel,
    GoBack,
    TheQuotes,
  },
  data() {
    return {
      selected: [],
      options: [
        { text: "Una pàgina web (500 €)", value: 500, panel: false },
        { text: "Una consultoria SEO (300 €)", value: 300, panel: false },
        {
          text: "Una campanya de Google Ads (200 €)",
          value: 200,
          panel: false,
        },
      ],
      pages: 1,
      languages: 1,
      formQuotes: ["Nom del pressupost", "Usuari"],
      quoteData: [],
      quote: [],
      filtersort: "",
    };
  },
  computed: {
    total() {
      if (this.selected.length != 0) {
        let values = [];
        this.selected.forEach((index) =>
          values.push(this.options[index].value)
        );
        return (
          values.reduce((total, amount) => total + amount) +
          this.pages * this.languages * 30
        );
      } else {
        return 0;
      }
    },
    orderBy() {
      return this.quote;
    },
  },
  methods: {
    dataPanel(pages, languages) {
      this.pages = pages;
      this.languages = languages;
    },
    whichIs: function (index) {
      let visible = this.options[0].panel;
      if (index === 0 && visible === false) {
        this.options[0].panel = true;
        this.pages = 1;
        this.languages = 1;
      }
      if (index === 0 && visible === true) {
        this.options[0].panel = false;
        this.pages = 0;
        this.languages = 0;
      }
    },
    saveQuote(event) {
      console.log("llegando");
      event.preventDefault();
      if (this.isValidated()) {
        let services = [];
        this.selected.forEach((index) =>
          services.push(this.options[index].text)
        );
        let quote = {
          quote: this.quoteData[0],
          user: this.quoteData[1],
          choose: services,
          total: this.total,
          date: new Date(),
        };
        this.quote.push(quote);
        console.log(`presupostos guardats: ${this.quote}`);
        this.resetForm();
      }
    },
    sortedBy(value) {
      console.log(`valor de l'emit: ${value}`);
      if (value == "reset") {
        this.orderBy = this.quote;
        console.log(this.orderBy);
      }
    },
    isValidated() {
      console.log("Ha intentat validar");
      if (!this.selected.length == 0 && this.quoteData.length == 2) {
        console.log("diu tot bé");
        console.log(this.selected);
        console.log(this.quoteData);
        return true;
      } else {
        console.log("diu error");
        console.log(this.selected);
        console.log(this.quoteData);
        return false;
      }
    },
    resetForm() {
      this.selected = [];
      this.quoteData = [];
      console.log("métode reset");
      console.log(this.options[0].panel);
      if (this.options[0].panel == true) {
        this.options[0].panel = false;
      }
      console.log(this.options[0].panel);
    },
  },
};
</script>
<style lang="css">
.home {
  width: 100%;
}
.movin-enter-active,
.movin-leave-active {
  transition: opacity 0.3s ease;
}
.movin-enter,
.movin-leave-to {
  opacity: 0;
}
</style>
