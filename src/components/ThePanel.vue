<template>
  <div class="panel">
    <b-row
      class="my-3"
      v-for="(option, index) in options"
      
      :key="option.id"
      v-model="option.id"
    >
      <b-col>
        <div>{{ option.text }}</div>
      </b-col>
      <b-col>
        <TheButton @addExtras="sendExtras" 
        :buttonId="index"
        :modalText="modalMessage[index].text" />
      </b-col>
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
      modalMessage: [
        { text: "Indica el número de pàgines que vols que tingui el teu lloc web" },
        { text: "Indica a quants idiomes vols tradïr el teu lloc web"},
      ]
      
    };
  },

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
    showTextModal(index) {
      
    }
  },
};
</script>

<style lang="sass">
  .panel
    border: 2px solid black
    border-radius: 1rem
    padding: 2rem 1rem
    margin: 1rem
    transform: scale(0)
    transition: 3000ms ease-in-out
    transform: scale(1)
    </style>
