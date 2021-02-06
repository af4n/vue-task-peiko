<template>
  <div id="app">
    <button @click="getData()" :disabled="isLoadedData">Get data</button>
    <div class="loading" v-if="isLoading">Loading...</div>
    <DataTable :data="data" v-if="data.length"/>
    <div class="error" v-if="isError">No data</div>
  </div>
</template>

<script>
  import DataTable from './components/DataTable.vue'
  import {payload} from './mocData/index.js'
  import getDataFunc from "./plugins/getDataFunc";

  export default {
    name: 'App',
    components: {
      DataTable
    },
    data() {
      return {
        data: [],
        isLoading: false,
        isError: false,
        isLoadedData: false
      }
    },
    methods: {
      async getData() {
        this.isLoading = true
        await getDataFunc(payload)
          .then((response) => {
            const {stocks, current, start} = response
            for (let i = 0; i < stocks.length; i++) {
              this.data.push({
                'stocks': stocks[i],
                'current': current[i],
                'start': start[i]
              })
            }
            this.isLoading = false
            this.isError = false
            this.isLoadedData = true

            console.log(this.data)
          })
          .catch((error) => {
            this.isLoading = false
            this.isError = true

            console.log(error)
          })
      }
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 60px;

    .loading, .error {
      margin-top: 10px;
    }

    button {
      padding: 8px 30px;
      background-color: #e3e3e3;
      border: 1px solid #9e9e9e;
      font-weight: bold;
      font-size: 16px;
    }
  }
</style>
