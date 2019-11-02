<template>
  <div class="col-sm-6 col-md-4 mt-4">
    <div class="card">
      <div class="card-header bg-secondary text-light">
        <h4>
          {{stock.name}}
          <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
        </h4>
      </div>
      <div class="card-body row">
        <div class="col-md-6">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger: insufficientFunds}">
        </div>
        <div class="col-md-6" style="text-align: right">
          <button class="btn btn-success" @click="sellPortStock" :disabled="insufficientQuantity || quantity <= 0 || Number.isInteger(quantity)">{{insufficientQuantity ? 'Not enough Stocks' : 'Sell'}}</button>
        </div>
      </div>
    </div>
  </div>    
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity () {
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
    ...mapActions([
      'sellStock'
    ]),
    sellPortStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      // eslint-disable-next-line no-console
      console.log(order, '...ord')
      this.sellStock(order)
      this.quantity = 0
    }
  }
}
</script>

<style scoped="">
  .danger {
    border: 1px solid red;
  }
</style>

