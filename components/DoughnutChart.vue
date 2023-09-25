<template>
    <div>
      <v-card>
        <v-card-title>Participation Chart</v-card-title>
        <v-card-text>
          <canvas ref="doughnutChart" class="chart-canvas"></canvas>
        </v-card-text>
      </v-card>
    </div>
  </template>
  
  <script>
  import { Doughnut } from "vue-chartjs";
  import Chart from "chart.js/auto"; // Importe 'chart.js/auto' para garantir compatibilidade
  
  export default {
    extends: Doughnut,
    props: ["data"],
    computed: {
      chartData() {
        return {
          labels: this.data.map((item) => item.firstName),
          datasets: [
            {
              backgroundColor: [
                "#FF5733",
                "#33FF57",
                "#5733FF",
                "#FF33E7",
                "#33E7FF",
                "#E7FF33",
                "#FF33A6",
                "#33A6FF",
                "#A6FF33",
              ],
              data: this.data.map((item) => item.participation),
            },
          ],
        };
      },
    },
    mounted() {
      const context = this.$refs.doughnutChart.getContext("2d");
  
      if (this.chartData) {
        new Chart(context, {
          type: "doughnut",
          data: this.chartData,
        });
      }
    },
  };
  </script>
  
  <style scoped>
  .chart-canvas {
    width: 10; /* Defina a largura desejada */
    height: 10px; /* Defina a altura desejada */
  }
  </style>