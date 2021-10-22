<template>
  <div class="cart">
      <SloganMenu/>
      <div class="cart--container">
           <h2 class="title">This is your cart</h2>
           <router-link to="/" class="back">←️ Back</router-link>
      </div>
      <div class="cart--content">
          <p class="emptyCar" v-if="hasNoItem">Your shopping cart is empty</p>
          <CartItem v-for="item in cartList" :key="item.id"
      :item="item" class="item"
      />
      <div class="cart--total" v-if="!hasNoItem"> 
          <span class="total">Total:</span>
          <span class="price">{{getCartTotal | currency}} <span class="or">or</span> </span>
          <p class="part">5x <span class="of">of</span>  {{getCartTotal / 5 | currency}}</p>
      </div>
      </div>
      <div class="button-container">
          <button class="checkout" @click="goToPayment" :disabled=" hasNoItem">Checkout</button>
      </div>
    
  </div>
</template>

<script>
import SloganMenu from './SloganMenu.vue'
import CartItem from './CartItem.vue'
import {  mapGetters} from 'vuex'



export default {
    name: 'Cart',
    components: {
        SloganMenu,
        CartItem,
    },
      methods: {
        goToPayment() {
           this.$router.push({name: 'Payment'})
        }
    },
    computed: {
        ...mapGetters([
            'getCartTotal'
        ]),
        cartList() {
            return this.$store.state.cartList;
        },
           hasNoItem() {
            return !this.cartList.length;
        },
    },
    filters: {
    currency(value) {
      return `R$${value.toLocaleString("pt-br", {
        minimumFractionDigits: 2,
      })} `;
    },
  
  },
   
}
</script>

<style scoped lang="less">
    .cart {
        min-height: 100vh;
        display: flex;
        flex-direction: column;

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

        &--content {
            flex-grow: 1;

            .emptyCar {
                text-align: center;
                font-size: 1.6rem;
                margin: 40px;
            }
            
        }

        .item {
            margin: 30px auto;
        }

        &--total {
           text-align: right;
           margin: 50px;

           .total {
               font-weight: 600;
               margin-right: 5px;
           }

           .price, .part   {
               color: @blue;
               font-weight: 600;
           }

           .part {
               margin-top: 0
           }
           .or, .of {
               color: black;
               font-weight: 500;
           }
        
        }

        .button-container {
            display: flex;
            justify-content: center;

            .checkout {
                width: 350px;
                margin: 30px;
                padding: 8px;
                border-radius: 8px;
                border: none;
                background: @blue;
                color: white;
                font-weight: 600;

                &:disabled {
                    background: @light-grey;
                    color: grey;
                }
            }
            
        }
            
    }
</style>