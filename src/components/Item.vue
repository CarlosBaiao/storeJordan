<template>
  <div class="item" @click="addToCart">
    <div class="item--tag" v-if="item.offer">OFFER</div>
    <div class="item--img-container">
      <img :src="imagePath" />
    </div>
    <h2 class="item--name">{{ item.name }}</h2>
    <p class="item--style">{{ item.style }}</p>
    <p class="item--size">{{ item.size }}</p>
    <p class="item--price">{{ item.price | currency }}</p>
    <p class="item--part">5x de {{ (item.price / 5) | currency }}</p>
  </div>
</template>

<script>
export default {
  name: "Item",
  props: {
    item: {},
  },
  filters: {
    currency(value) {
      return `R$ ${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })} `;
    },
  },
  computed: {
    imagePath() {
      return require(`../assets/images/${this.item.id}.jpg`);
    },
  },
  methods: {
    addToCart() {
       this.$store.dispatch('addToCart', this.item)

    }
  }
};
</script>

<style scoped lang="less">
.item {
  border: 2px solid @blue;
  width: 280px;
  border-radius: 8px;
  position: relative;
  margin: 10px;
  cursor: pointer;

  &--tag {
    position: absolute;
    background: @gold;
    border-radius: 8px;

    top: 15px;
    right: 15px;
    font-weight: 500;
    font-size: 12px;
    padding: 3px 8px;
  }

  &--img-container {
    background: @light-grey;
    border-radius: 8px 8px 0 0;
    width: 100%;

    img {
      width: 200px;
      display: block;
      margin: auto;
    }
  }

  &--name {
    font-weight: 600;
    font-size: 18px;
    padding: 0 20px;
  }
  &--style {
    color: @dark-grey;
    font-weight: 300;
    padding: 0 20px;
  }

  &--size {
    border: 2px solid @blue;
    border-radius: 8px;
    width: 35px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: @blue;
    margin: 0 20px;
  }
  &--price {
    font-size: 18px;
    font-weight: 600;
    color: @blue;
    padding: 0 20px;
    margin-bottom: 0;
  }

  &--part {
    color: @blue;
    font-size: 14px;
    padding: 0 20px;
    margin-top: 0;
  }

  @media @smartphones {
    img {
      border-radius: 8px 8px 0 0;
    }
  }
}
</style>
