<template>

  <div class="button">
    <b-button
      size="sm"
      @click="
        quantity++;
        sendData();
      "
    >
      +
    </b-button>
    <b-form>
      <b-form-input class="quantity" type="text" v-model="quantity" />
    </b-form>
    <b-button
      @click="
        quantity--;
        sendData();
      "
    >
      - </b-button
    ><b-icon
      class="icon"
      icon="info-circle-fill"
      @click="modal"
      variant="secondary"
    ></b-icon>
    <b-modal ref="my-modal" centered
    hide-footer hide-header>
      <div class="d-block text-center">
        <h4>{{ modalText }}</h4>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "TheButton",
  props: ['buttonId', 'modalText'],
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    sendData() {
      if (this.quantity <= 1) {
        this.quantity = 1;
      }
      this.$emit("addExtras", this.quantity, this.buttonId);
    },
    modal() {
      this.$refs["my-modal"].show();
    },
    // selectModal() {
    //   this.$emit("modalSelectText")
    // }
  },
};
</script>

<style scoped>
.button {
  display: flex;
  justify-content: center;
}
.btn-secondary {
  background-color: coral !important;
}
.quantity {
  border: none;
  outline: none;
  padding: 0 2rem;
  line-height: 2rem;
}
.icon {
  padding: 0.5rem;
  width: 2.5rem;
  height: 2.5rem;
}
.icon:hover {
  cursor: pointer;
}


/* input.form-control {
  width: 40%;
  text-align: left
} */
</style>
