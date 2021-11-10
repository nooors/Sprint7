<template>
<!-- Header -->
  <div class="home">
    <b-row class="text-left mt-3">
      <b-col>
        <h3>Pressupostos App</h3>
        <hr />
      </b-col>
    </b-row>

    <b-row>
      <!-- Services select form -->
      <b-col class="form">
        <b-form @submit="saveQuote">
          <b-form-group v-slot="{ ariaDescribedby }">
            <b-row
              align-h="start"
              v-for="(option, index) in options"
              :key="option.id"
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
        <the-quotes :dataQuotes="quote" @sortQuote="sortedBy" />
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
      selected: [], // Store the index of selected fields
      options: [   // Data for select form
        { id:1, text: "Una pàgina web (500 €)", value: 500, panel: false },
        { id:2, text: "Una consultoria SEO (300 €)", value: 300, panel: false },
        {
          id:3, text: "Una campanya de Google Ads (200 €)",
          value: 200,
          panel: false,
        },
      ],
      pages: 1,    // Data from The Panel component
      languages: 1,   // Data from The Panel component 
      formQuotes: ["Nom del pressupost", "Usuari"],    // Data for input labels
      quoteData: [],    // Data from input form
      quote: [],   // Array that stores the saved quotes. Each object represents one quote
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
    // orderBy() {
    //   return this.quote;
    // },  // Trying to update data from The Panel component
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
        this.resetForm();
      }
    },
    sortedBy(value) {
      if (value == "reset") {
        this.orderBy = this.quote;
      }
    },
    isValidated() {
      if (!this.selected.length == 0 && this.quoteData.length == 2 &&  !this.quote.includes(this.quoteData[0])) {
        return true;
      } else {  
        return false;
      }
    },
    resetForm() {
      this.selected = [];
      this.quoteData = [];
      this.languages = 1;
      this.pages = 1;
      if (this.options[0].panel == true) {
        this.options[0].panel = false;
      }
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
