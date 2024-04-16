<template>
  <v-container>
    <v-btn @click="this.estrai()" class="mb-3">clicca</v-btn>
    <!-- <p v-if="this.sx.length > 0">Sx {{ this.sx[this.p - 1] }}</p> <br>
    <p v-if="this.dx.length > 0">Dx {{ this.dx[this.p - 1] }}</p> -->

    <v-row>
      <v-col>
        <v-card class="mx-auto" max-width="400" v-if="this.sx.length">
          <v-img class="align-end text-white" height="200" :src="this.sx[this.p - 1].images[0]" cover>

          <!-- <v-img class="align-end text-white" height="200" :src="this.sx[this.p - 1].images[0]" cover> -->
            <v-card-title>{{ this.sx[this.p - 1].title }}</v-card-title>
          </v-img>

          <v-card-subtitle class="pt-4">
            {{ this.sx[this.p - 1].description }}
          </v-card-subtitle>

          <v-card-text>
            <div>
              <v-list>
                <v-list-subheader>Categoria</v-list-subheader>
                <v-list-item :prepend-avatar="this.sx[this.p - 1].category.image" 
                  :title="this.sx[this.p - 1].category.name">
                </v-list-item>
              </v-list>
            </div>
            <div>Prezzo: € {{ this.sx[this.p - 1].price }}</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange" text="Vota"></v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
      <v-col>
        <v-card class="mx-auto" max-width="400" v-if="this.dx.length">
          <v-img class="align-end text-white" height="200" :src="this.dx[this.p - 1].images[0]" cover>

          <!-- <v-img class="align-end text-white" height="200" :src="this.sx[this.p - 1].images[0]" cover> -->
            <v-card-title>{{ this.dx[this.p - 1].title }}</v-card-title>
          </v-img>

          <v-card-subtitle class="pt-4">
            {{ this.dx[this.p - 1].description }}
          </v-card-subtitle>

          <v-card-text>
            <div>
              <v-list>
                <v-list-subheader>Categoria</v-list-subheader>
                <v-list-item :prepend-avatar="this.dx[this.p - 1].category.image" 
                  :title="this.dx[this.p - 1].category.name">
                </v-list-item>
              </v-list>
            </div>
            <div>Prezzo: € {{ this.dx[this.p - 1].price }}</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange" text="Vota"></v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>

export default {
  name: 'HomeView',
  data() {
    return {
      prodotti: [],
      show: false,
      estratti: [],
      disponibili: [],
      sx: [],
      dx: [],
      pos: 0,
      p: 0
    }

  },
  methods: {
    async getProdotti() {
      await fetch('https://api.escuelajs.co/api/v1/products?offset=0&limit=64')
        .then(response => response.json())
        .then(data => {
          this.prodotti = data;
          console.log(this.prodotti);
        })
        .then(() => {
          this.prodotti.forEach(p => {
            this.disponibili.push(p);
          });
        });
    },
    estrai() {

      //get lunghezza di disponibili
      for (let i = 0; i < 2; i++) {
        let numero = this.disponibili.length;
        if (numero == 0) {
          console.log('finiti i prodotti');
          return;
        }
        console.log(numero);
        let random = Math.floor(Math.random() * numero);
        this.estratti.push(this.disponibili[random]);
        this.disponibili.splice(random, 1);
        if (i == 0) {
          this.sx.push(this.estratti[this.pos]);
        }
        else {
          this.dx.push(this.estratti[this.pos + 1]);
        }

      }
      this.pos = this.pos + 2;
      this.p = this.p + 1;

    },


  },
  created() {
    this.getProdotti();
  },
  mounted() {

  }




}
</script>
