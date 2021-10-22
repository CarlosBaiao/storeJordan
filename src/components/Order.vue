<template>
  <div class="order">
    <form>
      <div class="user-data">
        <p class="section-title">Your data</p>
        <div class="input-field">
          <label for="">{{ formData.name.label }}</label>
          <input
            type="text"
            :placeholder="formData.name.placeholder"
            v-model="formData.name.value"
            @blur="formData.name.isValid()"
            :class="{ error: !formData.name.valid }"
          />
          <p class="error-messege" v-if="!formData.name.valid">
            {{ formData.name.errorMessege }}
          </p>
        </div>
        <div class="input-field">
          <label for="">{{ formData.cellphone.label }}</label>
          <input
            type="text"
            :placeholder="formData.cellphone.placeholder"
            v-mask="'(##) #####-####'"
            v-model="formData.cellphone.value"
            @blur="formData.cellphone.isValid()"
            :class="{ error: !formData.cellphone.valid }"
          />
          <p class="error-messege" v-if="!formData.cellphone.valid">
            {{ formData.cellphone.errorMessege }}
          </p>
        </div>
      </div>
      <div class="address">
        <p class="section-title">Address</p>
        <div class="address-card" v-if="hasAddressInfo">
            <p>{{formData.city.value}} - {{formData.cep.value}}</p>
            <p>{{formData.street.value}}, {{formData.number.value}}</p>
        </div>
        <a @click="onShowAddressModal">{{addressButtonLabel}}</a>
      </div>

      <div class="payment">
            <p class="section-title">Payment</p>
            <p class="description">payment method:</p>
            <div class="radio-container">
                <div class="radio-options">
                    <input type="radio"  name="payment-type" id="card" value="card" v-model="paymentType">
                    <label for="card">Card</label>
                </div>
                    <div class="radio-options">
                    <input type="radio" name="payment-type" id="cash" value="cash">
                    <label for="cash">Cash</label>
                </div>
            </div>
      </div>
    </form>
    <button class="finishShopping" @click="orderItens">Complete buy</button>
    <Modal :show="showAddressModal" @on-modal-close="hideAddressModal">
      <div class="modal-content">
        <h1>Add address</h1>
        <div class="input-field">
          <label for="">{{ formData.cep.label }}</label>
          <input
            type="text"
            :placeholder="formData.cep.placeholder"
            v-model="formData.cep.value"
            @blur="formData.cep.isValid()"
            :class="{ error: !formData.cep.valid }"
          />
          <p class="error-messege" v-if="!formData.cep.valid">
            {{ formData.cep.errorMessege }}
          </p>
        </div>
        <div class="input-field">
          <label for="">{{ formData.city.label }}</label>
          <input
            type="text"
            :placeholder="formData.city.placeholder"
            v-model="formData.city.value"
            @blur="formData.city.isValid()"
            :class="{ error: !formData.city.valid }"
          />
          <p class="error-messege" v-if="!formData.city.valid">
            {{ formData.city.errorMessege }}
          </p>
        </div>
        <div class="address-container">
          <div class="input-field">
            <label for="">{{ formData.street.label }}</label>
            <input
              type="text"
              :placeholder="formData.street.placeholder"
              v-model="formData.street.value"
              @blur="formData.street.isValid()"
              :class="{ error: !formData.street.valid }"
            />
            <p class="error-messege" v-if="!formData.street.valid">
              {{ formData.street.errorMessege }}
            </p>
          </div>
          <div class="input-field">
            <label for="">{{ formData.number.label }}</label>
            <input
              type="text"
              :placeholder="formData.number.placeholder"
              v-model="formData.number.value"
              @blur="formData.number.isValid()"
              :class="{ error: !formData.number.valid }"
            />
            <p class="error-messege" v-if="!formData.number.valid">
              {{ formData.number.errorMessege }}
            </p>
          </div>
        </div>
        <button class="button-cancel" @click="hideAddressModal">Cancel</button>
        <button class="button-remove" @click="validateAddressForm">Add</button>
      </div>
    </Modal>
    <Modal :show="showInvalidAddressModal"  @on-modal-close="hideInvalidAddressModal">
      <div class="invalid-address-modal">
         <span v-html="warningIcon" class="icon"></span>
      <span>The address is mandatory</span>
      </div>
    </Modal>
  </div>
</template>

<script>
import Modal from "../components/Modal.vue";
import feather from 'feather-icons'

export default {
  components: {
    Modal,
  },
  data() {
    return {
      formData: {
        name: {
          value: "",
          placeholder: "Type your name",
          errorMessege: "The name is required",
          label: "Name*",
          valid: true,
          isValid: () => {
            this.formData.name.valid = !!this.formData.name.value.length;
          },
        },
        cellphone: {
          value: "",
          placeholder: "Type your cell phone",
          errorMessege: "The cell phone is required",
          label: "Cell phone*",
          valid: true,
          isValid: () => {
            this.formData.cellphone.valid =
              this.formData.cellphone.value.length === 15;
          },
        },
        cep: {
          value: "",
          placeholder: "Type your zip code",
          errorMessege: "The  zip code is required",
          label: "Zip code*",
          valid: true,
          isValid: () => {
            this.formData.cep.valid = !!this.formData.cep.value.length;
          },
        },
        city: {
          value: "",
          placeholder: "Type your city",
          errorMessege: "The zip code is required",
          label: "City*",
          valid: true,
          isValid: () => {
            this.formData.city.valid = !!this.formData.city.value.length;
          },
        },
        street: {
          value: "",
          placeholder: "Type your address",
          errorMessege: "The address is required",
          label: "Address*",
          valid: true,
          isValid: () => {
            this.formData.street.valid = !!this.formData.street.value.length;
          },
        },
        number: {
          value: "",
          placeholder: "Type your number",
          errorMessege: "The number is required",
          label: "Number*",
          valid: true,
          isValid: () => {
            this.formData.number.valid = !!this.formData.number.value.length;
          },
        },
      },
      showAddressModal: false,
      showInvalidAddressModal: false,
      paymentType: "card"
    };
  },
  computed: {
    warningIcon() {
      return feather.icons['alert-triangle'].toSvg();
    },
    isAddressFormValid() {
      let isValid = true;
      isValid &= this.formData.cep.valid;
      isValid &= this.formData.city.valid;
      isValid &= this.formData.street.valid;
      isValid &= this.formData.number.valid;
      return isValid;
    },
    isUserDataValiid() {
      let isValid = true;
      isValid &= this.formData.name.valid;
      isValid &= this.formData.cellphone.valid;
      return isValid;
    },
    hasAddressInfo() {
        return (
        this.formData.cep.value ||
        this.formData.city.value ||
        this.formData.street.value ||
        this.formData.number.value
        )
        
    },
    addressButtonLabel() {
        return this.hasAddressInfo ? 'Edit address' : 'Add address'
    }
  },    
  methods: {
    triggerValidations() {
      this.formData.name.isValid();
      this.formData.cellphone.isValid();
      this.triggerAddressValidations();
      this.showInvalidAddressModal = !this.isAddressFormValid;
    }, 
    triggerAddressValidations() {
      this.formData.cep.isValid();
      this.formData.city.isValid();
      this.formData.street.isValid();
      this.formData.number.isValid();
    },
    orderItens() {
      this.triggerValidations();
      if(!this.isAddressFormValid || !this.isUserDataValiid) return;
      this.resetCart()
      this.goToSuccess()
    },
    onShowAddressModal() {
      this.showAddressModal = true;
    },
    hideAddressModal() {
      this.showAddressModal = false;
    },
    validateAddressForm() {
      this.triggerAddressValidations();
      if (!this.isAddressFormValid) return;
      this.showAddressModal = false;
    },
    goToSuccess(){
      this.$router.push({name: 'Success'})
    },
    hideInvalidAddressModal() {
      this.showInvalidAddressModal = false
    },
     resetCart() {
          return this.$store.state.cartList = 0;
        }
  },
};
</script>

<style lang="less" scoped>
.order {
  width: 720px;
  border-radius: 8px;
  border: 2px solid @blue;
  padding: 30px 50px;
  margin: 30px auto;

  form {
    display: flex;
    flex-direction: column;
  }

  .input-field {
    display: flex;
    flex-direction: column;

    label {
      font-weight: 500;
      font-size: 16px;
      margin-bottom: 5px;
    }

    & + .input-field {
      margin-top: 15px;
    }

    
  }
  .section-title {
      font-weight: 600;
      font-size: 22px;
      margin-bottom: 20px;
    }

  .finishShopping {
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

  .error-messege {
    font-size: 12px;
    color: @error-color;
  }

  .address {
    a {
      color: @blue;
      text-decoration: underline;
      cursor: pointer;
      font-size: 15px;
    }

    .address-card {
        border-radius: 8px;
        border: 2px solid @light-grey;
        padding: 10px;
        margin: 15px 0;
        width: fit-content;
        font-weight: normal;
        color: @dark-grey;
        font-size: 13px;
       
    }

  }

  .address-container {
    display: flex;
    align-items: center;
    margin: 15px 0;
    

    .input-field {
      margin: 0;
      width: 100%;

      & + .input-field {
        width: 30%;
        margin-left: 15px;
      }
    }
  }
  .button-cancel,
  .button-remove {
    padding: 5px 15px;
    font-weight: 600;
  }

  .button-remove {
    background: @blue;
    color: white;
  }

  button {
    background: none;
    border: 2px solid @blue;
    height: 47px;
    width: 100px;
    border-radius: 8px;
    margin: 0 5px;
  }

  .payment {
      .description {
          margin:  0;
      }
    .radio-container {
        display: flex;
        
        .radio-options {
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 500;
           
           label {
               margin-left: 4px;
           }
            

            & + .radio-options {
            margin: 10px;
            }
        }
    }
  }


  .invalid-address-modal {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding-bottom: 20px;
    
    .icon {
      margin-bottom: 10px;
    }
  }
  @media @tablets {
    width: 480px;

    .address-container {
      flex-direction: column;

       .input-field + .input-field {
         width: 100%;
       }
    }
  }

  @media @smartphones {
    width: 300px;

    .finishShopping {
      width:200px;
    }
  }
}
</style>
