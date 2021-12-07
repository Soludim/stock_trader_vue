<template>
  <nav class="navbar navbar-default">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">Stock Trader</router-link>

      <div class="collapse navbar-collapse">
        <ul class="nav navbar-nav">
          <router-link to="/portfolio" tag="li" activeClass="active">
            <a>Portfolio</a>
          </router-link>
          <router-link to="/stocks" tag="li" activeClass="active">
            <a>Stocks</a>
          </router-link>
        </ul>
        <strong class="navbar-text navbar-right">Funds: {{funds | currency}}</strong>
        <ul class="nav navbar-nav navbar-right">
          <li>
            <a href="#" @click="endDay">End Day</a>
          </li>
          <li @click="isDropDown = !isDropDown" class="dropdown" :class="{open: isDropDown}">
            <a href="#" class="dropdown-toggle" data-toggle="dropdwon">
              Save & Load
              <span class="caret"></span>
            </a>
            <ul class="dropdown-menu animate__animated animate__bounceIn">
              <li>
                <a href="#" @click="saveData">Save Data</a>
              </li>
              <li>
                <a href="#" @click="loadData">Load Data</a>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  data() {
    return {
      isDropDown: false,
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
  methods: {
    endDay() {
      this.$store.dispatch("randomizeStocks");
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks,
      };
      this.$http.put("data.json", data);
    },
    loadData() {
      this.$store.dispatch("loadData");
    },
  },
};
</script>
<style scoped>
</style>