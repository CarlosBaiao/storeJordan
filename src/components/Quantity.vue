<template>
  <div class="quantity">
    <p class="item--quantity">
      <span class="price-description"> Quantity:</span>
      <button :disabled="item.quantity == 0" @click="onDecreaseButtonClick">
        -
      </button>
      {{ item.quantity }}
      <button @click="onIncreaseButtonClick">+</button>
    </p>
    <Modal :show="showModal" @on-modal-close="showModal = false">
      <div class="modal-content">
        <h2>Do you want to remove from cart?</h2>
        <div class="buttons">
          <button class="button-cancel" @click="onCancelButtonClick">Cancel</button>
          <button class="button-remove" @click="onRemoveButtonClick"> Yes, remove</button>
        </div>
      </div>
    </Modal>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import Modal from "./Modal.vue";
export default {
  props: {
    item: {},
  },
  components: {
    Modal,
  },
  data() {
    return {
      showModal: false,
    };
  },
  methods: {
    ...mapActions(["increaseQuantity", "decreaseQuantity"]),
    onDecreaseButtonClick() {
      this.decreaseQuantity(this.item.id);
      if (this.item.quantity === 0) this.showModal = true;
    },
    onIncreaseButtonClick() {
      this.increaseQuantity(this.item.id);
    },
    onCancelButtonClick() {
      this.increaseQuantity(this.item.id);
      this.showModal = false;
    },
    onRemoveButtonClick() {
      this.showModal = false
      this.$store.dispatch('removeFromCart', this.item.id)
    }
  },
};
</script>

<style lang="less" scoped>
.quantity {
  font-weight: 600;
  margin-bottom: 0;

  button {
    background: none;
    border: 2px solid @blue;
    padding: 0 5px;
    border-radius: 8px;
    margin: 0 5px;
  }

  @media @tablets {
    .price-description {
      display: none;
    }

    .item--quantity {
      margin: 0;
    }
  }

  .modal-content {

    h2 {
      text-align: center;
      margin: 20px 0;
    }
    .buttons {
      text-align: right;
    }

    .button-cancel, .button-remove {
      padding: 5px 15px;
      font-weight: 600;
      
    }

    .button-remove {
      background: @blue;
      color: white;
    }

    
  }
}
</style>
