<template>
  <b-container class="panel">
    <b-row
      class="my-2"
      v-for="(index, option) in options"
      :key="option.id"
      v-model="option.id"
    >
      <b-col sm-9>
        <div>{{ option.text }}</div>
      </b-col>
      <b-col sm-3>
        <TheButton @addExtras="sendExtras()" 
        :id="option.id" />
      </b-col>
    </b-row>

    <b-row>
      <!-- <TheButton @addExtras="saveExtras" /> -->
    </b-row>
  </b-container>
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
      webExtra: 1,
      options: [
        { id: "pages", text: "Número de pàgines", value: 1 },
        { id: "languages", text: "Número d'idiomes", value: 1 },
      ],
      dataExtras: [1, 1],
    };
  },

  computed: {},

  methods: {
    sendExtras(dataButton) {
      this.options.value == "pages"
        ? (this.dataExtras[0] = dataButton)
        : (this.dataExtras[1] = dataButton);
      this.$emit("extrasPanel", this.dataExtras);
      console.log(this.options.value)
    },

    // for(let i = 0; i < this.options.length-1; i++){
    //   this.dataExtras[i] = this.options[i].value
    // }
  },
};
</script>

<style></style>
