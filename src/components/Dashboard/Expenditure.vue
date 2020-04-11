<template>
  <div class="expenditure">
    <div
      class="expenditure--noData"
      v-if="Object.keys(expenditureData).length === 0"
    >
      <div class="expenditure--noData--heading">Expenditure</div>
      <div class="expenditure--noData--msg">NA</div>
    </div>
    <highcharts
      v-else
      class="expenditure--highchart"
      :options="chartOptions"
    ></highcharts>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";
export default {
  name: "Expenditure",
  data() {
    return {};
  },
  props: ["expenditures"],
  computed: {
    chartOptions() {
      return {
        chart: {
          type: "column"
        },
        credits: {
          enabled: false
        },
        title: {
          text: "Expenditure",
          style: {
            fontFamily: "sans-serif"
          }
        },
        xAxis: {
          categories: Object.keys(this.expenditureData)
        },
        yAxis: {
          min: 0,
          title: {
            text: "Amount (Rupees)",
            style: {
              fontFamily: "sans-serif"
            }
          },
          stackLabels: {
            enabled: true,
            style: {
              fontWeight: "bold",
              color: "black"
            }
          }
        },
        legend: {
          enabled: false
        },
        tooltip: {
          formatter: function() {
            return `${this.key}: ${this.y}`;
          }
        },
        plotOptions: {
          column: {
            stacking: "normal",
            dataLabels: {
              enabled: false
            }
          }
        },
        series: [
          {
            data: Object.values(this.expenditureData)
          }
        ]
      };
    },
    expenditureData() {
      return { ...this.expenditures };
    }
  },
  components: {
    highcharts: Chart
  }
};
</script>

<style lang="scss" scoped>
.expenditure {
  @include display-container(flex,center);
  @include flex-direction(column);
  padding: 2rem;
  grid-area: $grid-expenditure;
  background-color: $color-primary;
  &--noData {
    @include flex-direction(column);
         @include display-container(flex,center);
   
    height: 100%;
    font-size: 2rem;
    &--msg {
      // font-size: 2rem;
      padding: 3rem;
      color: white;
    }
  }

  &--highchart {
    @include width-height-100;
  }
}
</style>
