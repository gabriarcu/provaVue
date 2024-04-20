<template>
  <v-container>
    <v-card class="mb-3" style="border-color: white;" color="#202225" prepend-icon="mdi-ballot-recount-outline"
      subtitle="Prodotti e categorie">
      <template v-slot:title>
        <span class="font-weight-black">Statistiche</span>
      </template>
    </v-card>

    <v-card class="mx-auto mb-3" prepend-icon="mdi-trophy-outline" subtitle="Top" v-if="this.winner==null">
      <template v-slot:title>
        <span class="font-weight-black">Products & Categories</span>
      </template>

      <v-card-text class="bg-surface-light" height="350">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" color="#202225" dark max-width="500">
              <v-card-text>
                <v-row>
                  <v-col>
                    <v-card-title class="text-center">
                      <v-img class="text-white mt-4" max-height="500" max-width="500"
                        src="https://static.vecteezy.com/system/resources/previews/019/852/279/original/no-data-empty-data-concept-illustration-free-vector.jpg"
                        cover rounded="lg"></v-img>
                    </v-card-title>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-row>
      <v-col xs="12" sm="6">
        <v-card class="mx-auto mb-3" prepend-icon="mdi-trophy-outline" subtitle="Top" v-if="this.winner!=null">
          <template v-slot:title>
            <span class="font-weight-black">Products</span>
          </template>

          <v-card-text class="bg-surface-light">
            <v-row class="mb-10">
              <v-col>
                <apexchart type="bar" height="350" :options="chartOptions" :series="series"></apexchart>
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
      </v-col>
      <v-col xs="0" sm="6">
        <v-card class="mx-auto" prepend-icon="mdi-trophy-outline" subtitle="Top" v-if="this.winner!=null">
          <template v-slot:title>
            <span class="font-weight-black">Categories</span>
          </template>

          <v-card-text class="bg-surface-light">
            <v-row class="mb-10">
              <v-col>
                <apexchart type="bar" height="350" :options="chartOptions2" :series="series2"></apexchart>
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
                    <tr v-for="(item, index) in this.categorieOrdinate" :key="index" class="text-left">
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
      </v-col>
    </v-row>
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
      series2: [{
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
          convertedCatToNumeric: true,
          tickAmount: 1,
        }
      },
      chartOptions2: {
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
          convertedCatToNumeric: true,
          tickAmount: 1,
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
      this.prodottiOrdinati.forEach(item => (this.chartOptions.xaxis.categories).push(item.nome));
      this.categorieOrdinate.forEach(item => (this.chartOptions2.xaxis.categories).push(item.nome));
    },
    putQuantita() {
      this.prodottiOrdinati.forEach(item => (this.series[0].data).push(parseInt(item.quantita)));
      this.categorieOrdinate.forEach(item => (this.series2[0].data).push(parseInt(item.quantita)));

    },
    check() {
      if (this.winner != null) {
        const { prodottiOrdinati, categorieOrdinate } = this.contaProdottiECategorie();
        this.prodottiOrdinati = prodottiOrdinati;
        this.categorieOrdinate = categorieOrdinate;
        
        this.putLabel();
        this.putQuantita();
      }
    }
  },
  mounted() {
    //
  },
  created() {
    this.getWinner();
    this.check();

  },
}
</script>
