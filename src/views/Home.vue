<template>
  <div>
    <b-form-group
      label="Individual stacked checkboxes (default)"
      v-slot="{ ariaDescribedby }"
    >
      <b-form-checkbox
        v-for="option in options"
        v-model="selected"
        :key="option.value"
        :value="option.value"
        :aria-describedby="ariaDescribedby"
        name="flavour-3a"
      >
        {{ option.text }}
      </b-form-checkbox>
    </b-form-group>
    Preu: {{ totalBasic }}
    <ThePanel @extrasPanel="dataPanel()" />
    <div class="data__panel">
      {{ dataFromPanel }}
    </div>
    
    <div class="total_final">
      Total 
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import ThePanel from '../components/ThePanel.vue'

export default {
  name: "Home",
  components: {
    ThePanel,
  },
  data() {
    return {
      selected: [],
      options: [
        { text: "Una pàgina web (500 €)", value: 500 },
        { text: "Una consultoria SEO (300 €)", value: 300 },
        { text: "Una campanya de Google Ads (200 €)", value: 200 },
      ],
      dataFromPanel: [],
    };
  },
  computed: {
    totalBasic() {
      if(this.selected.length != 0){
        return this.selected.reduce((total, amount) => total + amount);
      } else {
        return 0;
      }
    },
    // Total(){
    //   return this.totalBasic + this.totalExtra;
    // },
    
  },
  methods: {
    dataPanel(data){
      this.dataFromPanel = data;
    }
  }
};
</script>
