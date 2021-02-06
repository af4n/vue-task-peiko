<template>
  <div class="container">
    <div class="table">
      <div class="thead">
        <div class="cell sort" @click="sortByStocks">Stock &#9660;</div>
        <div class="cell">Current</div>
        <div class="cell">Change</div>
      </div>
      <div class="tbody">
        <div class="col">
          <div class="cell"
               v-for="data in data"
               :key="data.index"
          >{{data.stocks}}
          </div>
        </div>
        <div class="col">
          <div class="cell"
               v-for="data in data"
               :key="data.index"
          >{{(data.current).toFixed(2)}}
          </div>
        </div>
        <div class="col">
          <div class="cell"
               v-for="data in data"
               :key="data.index"
               :class="(data.current - data.start).toFixed(2) >= 0 ? 'green' : 'red'"
          >{{(data.current - data.start).toFixed(2)}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      data: Array
    },
    methods: {
      sortByStocks() {
        this.data.sort((a, b) => a.stocks.localeCompare(b.stocks))
      }
    }
  }
</script>

<style lang="scss">
  .container {
    display: flex;
    justify-content: center;

    .table {
      width: 400px;
      margin-top: 20px;

      .thead {
        display: flex;
        background-color: #e3e3e3;
        border: 1px solid #9e9e9e;

        .cell {
          flex-grow: 1;
          font-weight: bold;
          padding-top: 5px;
          padding-bottom: 5px;
        }

        .sort {
          cursor: pointer;
        }
      }

      .tbody {
        display: flex;
        border: 1px solid #9e9e9e;
        border-top: none;

        .col {
          flex-grow: 1;

          .cell {
            border-bottom: 1px solid #9e9e9e;
            padding-top: 5px;
            padding-bottom: 5px;
          }

          .green {
            color: green;

            &:before {
              content: '+';
            }
          }

          .red {
            color: red
          }
        }
      }
    }
  }
</style>
