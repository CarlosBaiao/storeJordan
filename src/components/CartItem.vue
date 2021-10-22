<template>
  <div class="item">
    <img class="item--img" :src="imagePath" />
    <div class="content">
      <h3 class="item--name">{{ item.name }}</h3>
      <p class="item--size">
        Size: <span>{{ item.size }}</span>
      </p>
      <div class="item--priceAndQuantity">
        <p class="item--price">{{ item.price | currency }}</p>
        <Quantity :item="item" class="item--quantity"/>
      </div>
    </div>
   
  </div>
</template>

<script>
import Quantity from './Quantity.vue'
import { mapActions } from "vuex";


export default {
  name: "CartItem",
  components: {
    Quantity
  },
  props: {
    item: {},
  },
  data() {
    return {
      showModal: false,
    };
  },
  computed: {
    imagePath() {
      return require(`../assets/images/${this.item.id}.jpg`);
    },
  },
  filters: {
    currency(value) {
      return `R$ ${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })} `;
    },
  },
  methods: {
    ...mapActions(["increaseQuantity", "decreaseQuantity"]),
  },
};
</script>

<style lang="less" scoped>
.item {
  display: flex;
  border: 2px solid @blue;
  width: 600px;
  border-radius: 8px;

  &--img {
    width: 170px;
    border-radius: 8px 0 0 8px;
  }

  .content {
    padding: 0 20px;
    width: 100%;
  }

  &--size {
    color: @dark-grey;
    font-weight: 600;
    span {
      border: 2px solid @blue;
      border-radius: 8px;
      width: 35px;
      padding: 0 3px;
      margin-left: 5px;
      color: @blue;
    }
  }

  &--priceAndQuantity {
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

 

  &--price {
    font-size: 18px;
    font-weight: 600;
    color: @blue;
    margin-bottom: 0;
  }

  &--part {
    color: @blue;
    font-size: 14px;
    margin-top: 0;
  }

  @media @tablets {
    width: 500px;
  }

  @media @smartphones {
    width: 300px;
    display: flex;
    flex-direction: column;

    &--img {
      width: 296px;
      border-radius: 8px 8px 0 0;
    }

    &--size {
      margin: 0;
    }

    &--price {
      margin: 0;
    }
    

    &--priceAndQuantity {
      align-items: center;

      .price-description {
        display: none;
      }

      button {
        font-size: 1.2rem;
        font-weight: 600;
      }
    }
  }
}
</style>
