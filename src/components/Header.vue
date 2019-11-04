<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link to='/' class="navbar-brand" href="#">Stock Trader</router-link>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <router-link to="/portfolio" class="nav-item active" activeClass="active" tag="li">
          <a class="nav-link">Portfolio <span class="sr-only">(current)</span></a>
        </router-link>
        <router-link to="/stocks" class="nav-item" activeClass="active" tag="li">
          <a class="nav-link">Stocks</a>
        </router-link>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            Save & Load
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#">Save Data</a>
            <a class="dropdown-item" href="#">Load Data</a>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#">Something else here</a>
          </div>
        </li>
      </ul>
<!--       <form class="form-inline my-2 my-lg-0">
        <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
      </form> -->
      <div class="form-inline my-2 my-lg-0">
        <div class="nav-item mr-sm-2" activeClass="active">
          <a class="nav-link" @click="endDay">End Day <span class="sr-only">(current)</span></a>
        </div>
        <div class="nav-item dropdown my-2 my-sm-0" @click="isDropdownOpen = !isDropdownOpen">
          <div class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" :aria-expanded="isDropdownOpen">
            Save & Load
          </div>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown" :class="{show: isDropdownOpen}">
            <a class="dropdown-item" href="#">Save Data</a>
            <a class="dropdown-item" href="#">Load Data</a>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#">Something else here</a>
          </div>
        </div>
        <div>
          <span class="av-item mr-sm-2 strong-text">Funds: {{funds | currency}}</span>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
  import {mapActions} from 'vuex'

  export default {
    data () {
      return {
        isDropdownOpen: false
      }
    },
    computed: {
      funds () {
        return this.$store.getters.funds
      }
    },
    methods: {
      ...mapActions([
        'randomizeStocks'
      ]),
      endDay () {
        this.randomizeStocks()
      }
    }
  }
</script>
