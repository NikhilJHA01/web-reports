<template>
  <div class="income">
    <div class="income--noData" v-if="Object.keys(incomeData).length === 0">
      <div class="income--noData--heading">Monthly Income</div>
      <div class="income--noData--msg">NA</div>
    </div>
    <highcharts
      v-else
      class="income--highchart"
      :options="chartOptions"
    ></highcharts>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";

export default {
  name: "Income",
  props: ["income"],
  computed: {
    incomeData() {
      return { ...this.income };
    },
    chartOptions() {
      return {
        chart: {
          plotBackgroundColor: null,
          plotBorderWidth: null,
          plotShadow: false,
          type: "pie"
        },
        title: {
          text: "Monthly Income Distribution"
        },
        tooltip: {
          // pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>"
          formatter: function() {
            return `${this.key}: ${this.y}`;
          }
        },
        credits: {
          enabled: false
        },
        accessibility: {
          // point: {
          //   valueSuffix: "%"
          // }
        },
        plotOptions: {
          pie: {
            allowPointSelect: true,
            cursor: "pointer",
            dataLabels: {
              useHTML: true,
              formatter: function() {
                return `${this.point.name}: ${this.y}`;
              },
              overflow: "none",
              crop: false,
              reserveSpace: true
              // format: "<b>{point.key}</b>: {point.y} %"
            }
          }
        },
        series: [
          {
            name: this.incomeData ? this.incomeData["locality"] : "",
            colorByPoint: true,
            innerSize: "40%",
            data: [
              {
                name: this.incomeData ? this.incomeData["locality"] : "",
                y: this.incomeData ? this.incomeData["income"] : ""
              }
            ]
          }
        ]
      };
    }
  },
  components: {
    highcharts: Chart
  }
};
</script>

<style lang="scss" scoped>
.income {
     @include display-container(flex,center);
  @include flex-direction(column);
  background-color: $color-primary;
  padding: 0.5rem;
  grid-area: $grid-income;
  &--noData {
    @include flex-direction(column);
     @include display-container(flex,center);
    height: 100%;
    font-size: 2rem;
    padding:4rem;

    &--msg {
      // font-size: 2rem;
      padding: 3rem;
      color: white;
    }
  }

  &--highchart {
    @include width-height-100;
  }
  &--count {
    font-size: 2rem;
    color: $color-white;
  }
}
</style>
