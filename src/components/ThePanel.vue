<template>
  <div class="panel">
    <b-row
      class="my-3"
      v-for="(option, index) in options"
      
      :key="option.id"
      v-model="option.id"
    >
      <b-col sm-9 justfy-content-center>
        <div>{{ option.text }}</div>
      </b-col>
      <b-col sm-3 justify-content-center>
        <TheButton @addExtras="sendExtras" 
        :buttonId="index" />
      </b-col>
    </b-row>

    <b-row>
      <!-- <TheButton @addExtras="saveExtras" /> -->
    </b-row>
  </div>
</template>

<script>
import TheButton from "./TheButton.vue";
export default {
  components: {
    TheButton,
  },
  name: "ThePanel",
  props: {},
  data() {
    return {
      options: [
        { id: "pages", text: "Número de pàgines", value: 1 },
        { id: "languages", text: "Número d'idiomes", value: 1 },
      ],
      pages: 1,
      languages: 1,
    };
  },

  computed: {},

  methods: {
    sendExtras(amountButton, indexButton) {
      if(indexButton === 0){
       this.pages = amountButton;
      }else if(indexButton === 1){
        this.languages = amountButton;
      }
      this.$emit( 'extrasPanel', this.pages, this.languages );
      console.log(`quantitat${amountButton}${typeof amountButton}`);
      console.log('botó' + indexButton + typeof indexButton);
      console.log(this.pages);
      console.log(this.languages);
    },
  },
};
</script>

<style lang="sass">
  .panel
    border: 2px solid black
    border-radius: 1rem
    padding: 2rem 1rem
    margin: 1rem 
    </style>
