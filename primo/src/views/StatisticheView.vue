<template>
  <v-container>
    <v-card class="mb-3" style="border-color: white;" color="#202225" prepend-icon="mdi-ballot-recount-outline"
      subtitle="Prodotti e categorie">
      <template v-slot:title>
        <span class="font-weight-black">Statistiche</span>
      </template>
    </v-card>

    <v-card class="mx-auto" prepend-icon="mdi-trophy-outline" subtitle="Product & Category">
      <template v-slot:title>
        <span class="font-weight-black">Top</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <apexchart type="bar" height="350" :options="chartOptions" :series="series"></apexchart>
          </v-col>
          <v-col>
            <v-table height="350px" fixed-header>
              <thead>
                <tr>
                  <th class="text-left">
                    #
                  </th>
                  <th class="text-left">
                    Nome
                  </th>
                  <th class="text-left">
                    Voti
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in this.prodottiOrdinati" :key="index" class="text-left">
                  <td>{{ index + 1 }}</td>
                  <td>{{ item.nome }}</td>
                  <td>{{ item.quantita }}</td>
                </tr>
              </tbody>
            </v-table>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>



  </v-container>
</template>
<script>
// https://apexcharts.com/vue-chart-demos/bar-charts/basic/
export default {
  name: 'StatisticheView',
  data() {
    return {
      winner: [],
      prodottiOrdinati: [],
      categorieOrdinate: [],
      series: [{
        data: []
      }], 
      chartOptions: {
        chart: {
          type: 'bar',
          height: 350
        },
        plotOptions: {
          bar: {
            borderRadius: 4,
            horizontal: true,
          }
        },
        dataLabels: {
          enabled: false
        },
        xaxis: {
          categories: [],
        }
      },
    }
  },
  methods: {
    getWinner() {
      this.winner = JSON.parse(localStorage.getItem("winner"));
    },
    contaProdottiECategorie() {
      const datiVincitori = this.winner;

      // Oggetti per tenere traccia del conteggio dei prodotti e delle categorie
      const conteggioProdotti = {};
      const conteggioCategorie = {};

      // Conta quante volte sono presenti i prodotti e le categorie
      datiVincitori.forEach((vincitore) => {
        // Conteggio dei prodotti
        const prodottoId = vincitore.id;
        if (conteggioProdotti[prodottoId]) {
          conteggioProdotti[prodottoId].quantita++;
          conteggioProdotti[prodottoId].dettagli.push(vincitore);
        } else {
          conteggioProdotti[prodottoId] = {
            quantita: 1,
            nome: vincitore.title,
            dettagli: [vincitore]
          };
        }

        // Conteggio delle categorie
        const categoriaId = vincitore.category.id;
        const categoriaNome = vincitore.category.name;
        if (conteggioCategorie[categoriaId]) {
          conteggioCategorie[categoriaId].quantita++;
        } else {
          conteggioCategorie[categoriaId] = {
            nome: categoriaNome,
            quantita: 1
          };
        }
      });

      // Ordina i conteggi dei prodotti in modo decrescente per numero
      const prodottiOrdinati = Object.values(conteggioProdotti).sort((a, b) => b.quantita - a.quantita);

      // Ordina i conteggi delle categorie in modo decrescente per numero
      const categorieOrdinate = Object.values(conteggioCategorie).sort((a, b) => b.quantita - a.quantita);

      return { prodottiOrdinati, categorieOrdinate };
    },
    putLabel() {
      let cat = [];
      this.prodottiOrdinati.forEach(item => (this.chartOptions.xaxis.categories).push(item.nome));
      return cat;
    },
    putQuantita() {
      this.prodottiOrdinati.forEach(item => (this.series[0].data).push(item.quantita));
    
    },
  },
  mounted() {
    //
  },
  created() {
    this.getWinner();
    const { prodottiOrdinati, categorieOrdinate } = this.contaProdottiECategorie();
    this.prodottiOrdinati = prodottiOrdinati;
    this.categorieOrdinate = categorieOrdinate;
    this.putLabel();
    this.putQuantita();
  },
}
</script>
