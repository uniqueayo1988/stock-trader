<template>
  <div class="col-sm-6 col-md-4 mt-4">
    <div class="card">
      <div class="card-header bg-muted">
        <h4>
          {{stock.name}}
          <small>(Price: {{stock.price}})</small>
        </h4>
      </div>
      <div class="card-body row">
        <div class="col-md-6">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger: insufficientFunds}">
        </div>
        <div class="col-md-6" style="text-align: right">
          <button class="btn btn-success" @click="buyStock" :disabled="insufficientFunds || quantity <= 0 || Number.isInteger(quantity)">{{insufficientFunds ? 'Insufficient Funds' : 'Buy'}}</button>
        </div>
      </div>
    </div>
  </div>    
</template>

<script>
export default {
  props: ['stock'],
  data () {
    return {
      quantity: 0
    }
  },
  computed: {
    funds () {
      return this.$store.getters.funds
    },
    insufficientFunds () {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods: {
    buyStock () {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.$store.dispatch('buyStock', order)
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
