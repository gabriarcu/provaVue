<template>
  <v-container>
    <!-- <v-btn @click="this.estrai()" class="mb-3">clicca</v-btn> -->
    <!-- <p v-if="this.sx.length > 0">Sx {{ this.sx[this.p - 1] }}</p> <br>
    <p v-if="this.dx.length > 0">Dx {{ this.dx[this.p - 1] }}</p> -->
    <v-card class="mx-auto" v-if="this.primo == true" prepend-icon="mdi-home-floor-1" subtitle="Vota il tuo prodotto preferito">
      <template v-slot:title>
        <span class="font-weight-black">Primo Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length">
              <v-img class="align-end text-white" height="200" :src="this.getImage(this.sx[this.p - 1].images[0])"
                cover>

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
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length">
              <v-img class="align-end text-white" height="200" :src="this.getImage(this.dx[this.p - 1].images[0])"
                cover>

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
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="secondo" v-if="this.secondo == true" prepend-icon="mdi-home-floor-2"
      subtitle="Vota il tuo prodotto preferito">
      <template v-slot:title>
        <span class="font-weight-black">Secondo Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length">
              <v-img class="align-end text-white" height="200" :src="this.getImage(this.sx[this.p - 1].images[0])"
                cover>

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
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length">
              <v-img class="align-end text-white" height="200" :src="this.getImage(this.dx[this.p - 1].images[0])"
                cover>

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
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-dialog v-model="dialog" width="auto">
      <v-card max-width="400" prepend-icon="mdi-update"
        text="Preparati per il secondo Round" title="Info">
        <v-sheet class="pa-4 text-center mx-auto" elevation="12" max-width="600" rounded="lg" width="100%">
          <v-icon class="mb-5" color="success" icon="mdi-check-circle" size="112"></v-icon>

          <h2 class="text-h5 mb-6">Primo Round terminato!</h2>
<!-- 

          <v-divider class="mb-4"></v-divider>

          <div class="text-end">
            <v-btn class="text-none" color="success" variant="flat" width="90" rounded @click="this.dialog = true">
              Ok
            </v-btn>
          </div> -->
        </v-sheet>
      </v-card>
    </v-dialog>

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
      p: 0,
      voti: [],
      primo: true,
      secondo: false,
      dialog: false,
    }

  },
  methods: {
    async getProdotti() {
      await fetch('https://api.escuelajs.co/api/v1/products?offset=0&limit=64')
        .then(response => response.json())
        .then(data => {
          this.prodotti = data;
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
          
          this.dialog = true;
          this.primo = false;
          this.secondo = true;
          //aspeta 2 secondi
          setTimeout(() => {
            this.scrollSecondoSection();
          }, 1000);
          
          
          return;
        }
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
    getImage(immagine) {
      //console.log("prima: " + immagine);
      if (immagine.includes("[") && immagine.includes("]")) {
        // console.log('vero');
        // console.log("dopo: " + (immagine.replace("[", "")).replace("]", ""));
        return ((immagine.replace("[", "")).replace("]", "")).substring(1, ((immagine.replace("[", "")).replace("]", "")).length - 1);
      } else {
        // console.log("dopo: " + immagine)
        return immagine;
      }
    },
    vota(prodotto) {
      if (this.voti.includes(prodotto)) {
        console.log('fine');
        return;
      }
      this.voti.push(prodotto);
      this.estrai();
    },
    scrollSecondoSection() {
      // Trova l'elemento con id "secondo"
      const secondoSection = document.getElementById('secondo');

      // Controlla se l'elemento esiste
      if (secondoSection) {
        // Utilizza scrollIntoView per far scorrere la pagina fino all'elemento
        secondoSection.scrollIntoView({ behavior: 'smooth' });
      } else {
        console.error('Elemento con id "secondo" non trovato');
      }
    }

  },
  created() {
    this.getProdotti().then(() => {
      this.estrai();
    });

  },
  mounted() {

  }




}
</script>
