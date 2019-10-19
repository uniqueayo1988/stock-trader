<template>
  <div id="app" class="container">
    <app-header />
    <div class="row">
      <div class="col-md-12">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header'
export default {
  name: 'app',
  components: {
    appHeader: Header
  }
}
</script>

<style>
  body {
    padding: 30px;
  }
</style>
