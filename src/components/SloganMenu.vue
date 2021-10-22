<template>
  <div class="slogan-menu">
    <div class="slogan-menu--container">
      <h2 class="slogan-menu--title">Jordan Store</h2>
      <img
        class="slogan-menu--logo"
        src="../assets/images/logoJordan.png"
      />
      <router-link to="/Cart">
      <button class="slogan-menu--cart">Cart ({{cartList}})</button>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "SloganMenu",
   computed: {
        cartList() {

            return this.$store.state.cartList.length || 0;
        }
    },
};
</script>

<style scoped lang="less">
.slogan-menu {
  &--container {
    height: 120px;
    display: flex;
    align-items: center;
    justify-content: space-around;
  }

  &--title {
    width: 165px;
    font-size: 1.6rem;
    font-weight: 400;
  }

  &--logo {
    width: 165px;
    height: 100px;
  }

  &--cart {
    background: white;
    border: 2px solid @light-blue;
    width: 165px;
    padding: 8px 0;
    font-weight: 700;
  }

  @media @tablets {
    &--container {
      height: 80px;
    }

    &--title {
      display: none;
    }

    &--logo {
      height: 60px;
      width: 100px;
    }

    @media @smartphones {
      &--cart {
        width: 100px;
      }
    }
  }
}
</style>
