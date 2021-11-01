<template>
  <div>
    <GoBack />
    <b-row align-h="start">
      <b-form-group
        label="Individual stacked checkboxes (default)"
        v-slot="{ ariaDescribedby }"
      >
        <b-row
          align-h="start"
          v-for="(option, index) in options"
          :key="option.value"
        >
          <b-form-checkbox
            v-model="selected"
            @change="whichIs(index)"
            :value="option.value"
            :aria-describedby="ariaDescribedby"
            name="flavour-3a"
          >
            {{ option.text }}
          </b-form-checkbox>
          <b-row align-h="start" v-show="option.panel">
            <ThePanel @extrasPanel="dataPanel" />
          </b-row>
        </b-row>
      </b-form-group>

      <div class="total_final">Preu: {{ total }}</div>
    </b-row>
  </div>
</template>

<script>
// @ is an alias to /src
import ThePanel from "../components/ThePanel.vue";
import GoBack from "@/components/GoBack.vue";

export default {
  name: "Home",
  components: {
    ThePanel,
    GoBack,
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
    };
  },
  computed: {
    total() {
      if (this.selected.length != 0) {
        return (
          this.selected.reduce((total, amount) => total + amount) +
          this.pages * this.languages * 30
        );
      } else {
        return 0;
      }
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
        this.pages = 1;
      }
      if (index === 0 && visible === true) {
        this.options[0].panel = false;
        this.pages = 0;
        this.languages = 0;
      }
    },
  },
};
</script>
<style lang="sass" scoped></style>
