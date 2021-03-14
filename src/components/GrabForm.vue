<template>
  <form @submit.prevent="submitForm" class="wrapper">
    <!--Gift amount  part-->
    <div class="part">
      <div class="columns">
        <div class="column is-3">
          <h2>Gift information</h2>
        </div>
      </div>
      <div class="columns">
        <div class="column is-3">
          <h3 class="bold">Select gift amount</h3>
        </div>
      </div>
      <!--Gift amount -->
      <div class="gift-amount">
        <div class="columns">
          <div class="column buttons is-1">
            <b-button
              class="amount"
              v-on:click="selectAmount('10', false)"
              v-bind:class="this.order.amount == '10' ? 'is-info' : 'outlined'"
            >
              $10
            </b-button>
          </div>
          <div class="column buttons is-1">
            <b-button
              class="amount"
              v-on:click="selectAmount('20', false)"
              v-bind:class="this.order.amount == '20' ? 'is-info' : 'outlined'"
            >
              $20
            </b-button>
          </div>
          <div class="column buttons is-1">
            <b-button
              class="amount"
              v-on:click="selectAmount('30', false)"
              v-bind:class="this.order.amount == '30' ? 'is-info' : 'outlined'"
            >
              $30
            </b-button>
          </div>
          <div class="column buttons is-1">
            <b-button
              class="amount"
              v-on:click="selectAmount('40', false)"
              v-bind:class="this.order.amount == '40' ? 'is-info' : 'outlined'"
            >
              $40
            </b-button>
          </div>
          <div class="column buttons is-1">
            <b-button
              class="amount"
              v-on:click="selectAmount('custom', true)"
              v-bind:class="
                form.isCustomAmount == true ? 'is-info' : 'outlined'
              "
            >
              custom
            </b-button>
          </div>
        </div>
      </div>
      <!--Gift Custom amount -->
      <div class="columns" v-if="form.isCustomAmount">
        <div class="column is-5">
          <b-field label="" type="is-light">
            <b-input
              placeholder="Enter custom amount"
              v-model="order.amount"
              class="custom-amount"
              icon="currency"
            ></b-input>
          </b-field>
          <div
            v-if="!this.order.amount && form.isSubmitted && form.isCustomAmount"
            class="error"
          >
            *Please enter sender name
          </div>
        </div>
      </div>
    </div>
    <!--Delivery type part-->
    <div class="part">
      <!--Delivery types-->
      <div class="delivery-type">
        <div class="columns">
          <div class="column is-3">
            <h3>Delivery type</h3>
          </div>
        </div>
        <div class="columns">
          <div class="column is-3">
            <b-radio
              v-model="order.deliveryType"
              name="deliveryType"
              native-value="Personal"
              class="delivery-type-label"
              type="is-info"
            >
              Personal
            </b-radio>
          </div>
          <div class="column is-3">
            <b-radio
              v-model="order.deliveryType"
              name="deliveryType"
              native-value="Send as gift"
              class="delivery-type-label"
              type="is-info"
            >
              Send as gift
            </b-radio>
          </div>
        </div>
      </div>
      <!--show if delivery time is send as gift -->
      <div v-if="order.deliveryType == 'Send as gift'">
        <div class="columns">
          <div class="column is-6">
            <b-field label="Sender name" class="label" type="is-light">
              <b-input
                placeholder="Enter sender name"
                v-model="order.senderName"
                type="text"
              ></b-input>
            </b-field>
            <div v-if="!order.senderName && form.isSubmitted" class="error">
              *Please enter sender name
            </div>
          </div>
          <div class="column is-6">
            <b-field label="Recipient name" class="label" type="is-light">
              <b-input
                placeholder="Enter recipient name"
                v-model="order.recipientName"
                type="text"
              ></b-input>
            </b-field>
            <div v-if="!order.recipientName && form.isSubmitted" class="error">
              *Please enter recipient name
            </div>
          </div>
        </div>
      </div>
      <!--Recipient information -->
      <div>
        <div class="columns">
          <div class="column is-6">
            <b-field label="Recipient email" class="label" type="is-light">
              <b-input
                placeholder="Enter recipient email"
                v-model="order.recipientEmail"
                type="email"
              ></b-input>
            </b-field>
            <div v-if="!order.recipientEmail && form.isSubmitted" class="error">
              *Please enter recipient email
            </div>
          </div>
          <div class="column is-6">
            <b-field label="Recipient phone " class="label" type="is-light">
              <b-input
                placeholder="Enter recipient phone"
                v-model="order.recipientPhone"
                type="text"
              ></b-input>
            </b-field>
            <div v-if="!order.recipientPhone && form.isSubmitted" class="error">
              *Please enter recipient phone
            </div>
          </div>
        </div>
      </div>
    </div>
     <!--Delivery type part-->
    <div class="part">
      <div class="columns">
        <div class="column is-3">
          <h3 class="text-align-left bold">Delivery time</h3>
        </div>
      </div>
      <!--Delivery time types-->
      <div class="columns">
        <div class="column is-3 text-align-left">
          <b-radio
            v-model="order.deliveryTime"
            name="deliveryTime"
            native-value="Immediately"
            class="delivery-time-label"
            type="is-info"
          >
            Immediately
          </b-radio>
        </div>
        <div class="column is-2">
          <b-radio
            v-model="order.deliveryTime"
            name="deliveryTime"
            native-value="Custom"
            class="delivery-time-label"
            type="is-info"
          >
            Custom
          </b-radio>
        </div>
      </div>

      <!--Delivery time - custom -->
      <div class="columns" v-if="order.deliveryTime === 'Custom'">
        <div class="column is-6">
          <div class="is-type-custom-label bold">Delivery period</div>
          <b-field>
            <b-datepicker
              ref="datepicker"
              expanded
              placeholder="Select a date"
              v-model="order.date"
            >
            </b-datepicker>
            <b-button
              @click="$refs.datepicker.toggle()"
              icon-left="calendar"
            />
          </b-field>
          <div v-if="!order.date && form.isSubmitted" class="error">
            *Please enter delivery date
          </div>
        </div>
        <div class="column">
          <div class="is-type-custom-label bold">Delivery period</div>
          <b-button
            class="card_price"
            v-on:click="selectPeriod('Morning', false)"
            v-bind:class="
              this.order.period == 'Morning' ? 'is-info' : 'is-light'
            "
          >
            Morning
          </b-button>
          <b-button
            class="card_price"
            v-on:click="selectPeriod('Afternoon', false)"
            v-bind:class="
              this.order.period == 'Afternoon' ? 'is-info' : 'is-light'
            "
          >
            Afternoon
          </b-button>
          <b-button
            class="card_price"
            v-on:click="selectPeriod('Evening', false)"
            v-bind:class="
              this.order.period == 'Evening' ? 'is-info' : 'is-light'
            "
          >
            Evening
          </b-button>
        </div>
      </div>
      <!--Delivery time message-->
      <div class="columns">
        <div class="column is-12">
          <b-field label="Gift message" class="label" type="is-light">
            <b-input
              maxlength="200"
              type="textarea"
              v-model="order.message"
            ></b-input>
          </b-field>
          <div v-if="!order.message && form.isSubmitted" class="error">
            *Please enter message
          </div>
        </div>
      </div>
    </div>
    <!--Send button part-->
    <div class="part">
      <div class="columns">
        <div class="column is-12 level-right submit">
          <b-button native-type="submit" type="is-info">SEND</b-button>
        </div>
      </div>
    </div>
  </form>
</template>
<script>

export default {
  name: 'Grab',
  data () {
    return {
      order: {
        amount: '30',
        senderName: null,
        recipientName: null,
        deliveryType: 'Personal',
        recipientPhone: null,
        recipietnEmail: null,
        deliveryTime: 'Custom',
        date: null,
        period: 'Afternoon',
        message: null
      },
      form: {
        isCustomAmount: false,
        isSubmitted: false
      }
    }
  },
  methods: {
    selectAmount: function (amount, isCustomAmount) {
      this.order.amount = amount
      this.form.isCustomAmount = isCustomAmount
      if (amount === 'custom') {
        this.order.amount = ''
      }
    },
    selectPeriod: function (period) {
      this.order.period = period
    },
    submitForm: function () {
      if (this.order.deliveryType === 'Send as gift' && this.order.amount && this.order.senderName && this.order.deliveryType &&
       this.order.recipientName && this.order.recipientPhone && this.order.recipientEmail &&
       this.order.deliveryTime) {
        console.log(this.order)
        return alert(JSON.stringify(this.order))
      }
      if (this.order.deliveryType === 'Personal' && this.order.amount && this.order.deliveryType && this.order.recipientPhone && this.order.recipientEmail &&
       this.order.deliveryTime) {
        console.log(this.order)
        return alert(JSON.stringify(this.order))
      }
      this.form.isSubmitted = true
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
.wrapper {
  background-color: white;
}
.wrapper h2 {
  font-size: 18px;
  color: #1e2226;
  font-weight: 600;
}
.wrapper h3 {
  font-size: 15px;
  color: #3c4044;
  font-weight: bold;
}

.gift-amount button.amount {
  font-weight: 500;
  min-width: 8px;
  height: 36px;
  padding: 0 9px;
}
.label,
.delivery-type,
.delivery-time-label,
.delivery-type-label,
.is-type-custom-label {
  font-size: 14px;
  color: #3c4044;
  font-weight: 500;
  text-align: left;
}
.error {
  font-size: 12px;
  color: #f83c5e;
  font-weight: bold;
  text-align: left;
}
.text-align-left {
  text-align: left;
}
.bold {
  font-weight: bold !important;
}
.part {
  border: 1px solid #fbfbfc !important;
  padding: 10px;
}
.vertical-line {
  width: 1px;
  height: 60px;
  background-color: #f0f2f4;
}
.submit{
  text-align: right;
}
</style>
