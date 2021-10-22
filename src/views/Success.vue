<template>
  <div class="success">
    <SloganMenu />
    <div class="success--container">
      <div class="success--card">
        <div class="icon" v-html="successIcon"></div>
        <h2>your purchase was successful !!!</h2>
        <p>thanks for the purchase :)</p>
        <img
        class="logo"
        src="../assets/images/logoJordan.png"
      />
      </div>
      <button class="backShopping" @click="goHome">Go back to shopping</button>
    </div>
    
  </div>
</template>

<script>
import SloganMenu from "../components/SloganMenu.vue";
import feather from "feather-icons";

export default {
  name: "Success",
  components: {
    SloganMenu,
  },
  computed: {
    successIcon() {
      return feather.icons["check-circle"].toSvg();
    },
  },
  methods: {
    goHome(){
      this.$router.push({name: 'Home'})
    },
  }
};
</script>

<style lang="less" scoped>
.success {
  &--container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: calc(100vh - 120px);
  }

  &--card {
    width: 600px;
    height: 300px;
    border: 2px solid @blue;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

   
    }

    h2 {
        font-weight: 400;
        color: @blue;
        text-align: center;
    } 
    
    p {
        font-weight: 500;
        color: @dark-grey;
    }
      .logo {
      height: 80px;
      width: 120px;
    }

    .backShopping {
    display: block;
    width: 350px;
    margin: 30px auto;
    padding: 8px;
    border-radius: 8px;
    border: none;
    background: @blue;
    color: white;
    font-weight: 600;
  }

    @media @smartphones {
        &--card {
            width: 330px;
        }
    }
    
  
}
</style>
