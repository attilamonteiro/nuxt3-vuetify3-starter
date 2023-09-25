<template>
  <div>
    <nav>
      <input type="text" placeholder="First name" v-model="firstName" />
      <input type="text" placeholder="Last name" v-model="lastName" />
      <input type="number" placeholder="Participation" v-model="participation" />
      <button @click="addData">Send</button>
    </nav>

    <section>
      <h2>DATA</h2>
      <p>Lorem ipsum...</p>
    </section>

    <section>
      <div class="data-table">
        <table>
          <thead>
            <tr>
              <th>First name</th>
              <th>Last name</th>
              <th>Participation</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in tableData" :key="index">
              <td>{{ item.firstName }}</td>
              <td>{{ item.lastName }}</td>
              <td>{{ item.participation }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="doughnut-chart">
        <DoughnutChart :data="tableData" :key="chartKey" />
      </div>
    </section>
  </div>
</template>

<script>
import DoughnutChart from "@/components/DoughnutChart.vue";

export default {
  components: {
    DoughnutChart,
  },
  data() {
    return {
      firstName: "",
      lastName: "",
      participation: "",
      tableData: [],

      chartKey: 0, // Adicionamos uma chave para forçar a atualização do gráfico
    };
  },
  methods: {
    addData() {
      if (this.firstName && this.lastName && !isNaN(this.participation)) {
        const newData = {
          firstName: this.firstName,
          lastName: this.lastName,
          participation: parseFloat(this.participation),
        };
        this.tableData.push(newData);

        // Incrementamos a chave para forçar a atualização do gráfico
        this.chartKey++;

        this.firstName = "";
        this.lastName = "";
        this.participation = "";
      }
    },
  },
};
</script>
<style scoped>
.doughnut-chart {
  width: 10; /* Defina a largura desejada */
  height: 10px; /* Defina a altura desejada */
}
</style>
