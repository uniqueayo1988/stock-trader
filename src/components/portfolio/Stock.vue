<template>
  <div class="col-sm-6 col-md-4 mt-4">
    <div class="card">
      <div class="card-header bg-secondary text-light">
        <h4>
          {{stock.name}}
          <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
        </h4>
      </div>
      <div class="card-body">
        <div class="float-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity">
        </div>
        <div class="float-right">
          <button class="btn btn-success" @click="sellPortStock" :disabled="quantity <= 0 || Number.isInteger(quantity)">Sell</button>
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
