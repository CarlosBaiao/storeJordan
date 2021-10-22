<template>
  <div class="payment">
      <SloganMenu/>
        <div class="payment--container">
           <h2 class="title">Payment</h2>
           <router-link to="/cart" class="back">←️ Back</router-link>
      </div>
      <Order/>
  </div>
</template>

<script>

import SloganMenu from '../components/SloganMenu.vue'
import Order from '../components/Order.vue'

export default {
  name: "Payment",
  components: {
    SloganMenu,
    Order
  }

}
</script>

<style lang="less" scoped>
.payment {
   &--container {
            width: 100%;
            height: 100px;
            background: @light-grey;
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin-top: 30px;

            .title {
            color: @dark-grey;
            font-weight: 500;
            margin: 0;
            }

            .back {
                color: @dark-grey;
                font-weight: 500;
                font-size: 1.3rem;
                text-decoration: none;
            }

        }
}
 
</style>