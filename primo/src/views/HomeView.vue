<template>
  <v-container>
    <v-card class="mb-3" style="border-color: white;" color="#202225" prepend-icon="mdi-ballot-recount-outline"
      subtitle="Vota il tuo prodotto preferito">
      <template v-slot:title >
        <span class="font-weight-black">Best products</span>
      </template>
    </v-card>

    <v-card class="mx-auto" v-if="this.primo == true" prepend-icon="mdi-numeric-1-box-multiple-outline"
      :subtitle="'Estratti '+ this.estratti.length + '/'+ this.disponibili.length + ' Disponibili'">
      <template v-slot:title>
        <span class="font-weight-black">Primo Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length" @click="this.vota(this.sx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length" @click="this.vota(this.dx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="secondo" v-if="this.secondo == true" prepend-icon="mdi-numeric-2-box-multiple-outline"
      :subtitle="'Estratti '+ this.estratti.length + '/'+ this.disponibili.length + ' Disponibili'">
      <template v-slot:title>
        <span class="font-weight-black">Secondo Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length" @click="this.vota(this.sx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length" @click="this.vota(this.dx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="terzo" v-if="this.terzo == true" prepend-icon="mdi-numeric-3-box-multiple-outline"
      :subtitle="'Estratti '+ this.estratti.length + '/'+ this.disponibili.length + ' Disponibili'">
      <template v-slot:title>
        <span class="font-weight-black">Terzo Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length" @click="this.vota(this.sx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length" @click="this.vota(this.dx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="quarto" v-if="this.quarto == true" prepend-icon="mdi-numeric-4-box-multiple-outline"
      :subtitle="'Estratti '+ this.estratti.length + '/'+ this.disponibili.length + ' Disponibili'">
      <template v-slot:title>
        <span class="font-weight-black">Quarto Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length" @click="this.vota(this.sx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length" @click="this.vota(this.dx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="quinto" v-if="this.quinto == true" prepend-icon="mdi-numeric-5-box-multiple-outline"
      :subtitle="'Estratti '+ this.estratti.length + '/'+ this.disponibili.length + ' Disponibili'">
      <template v-slot:title>
        <span class="font-weight-black">Quinto Round</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.sx.length" @click="this.vota(this.sx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.sx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length" @click="this.vota(this.dx[this.p - 1])">
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

              <!-- <v-card-actions>
                <v-btn color="orange" text="Vota" @click="this.vota(this.dx[this.p - 1])"></v-btn>
              </v-card-actions> -->
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto mt-3" id="finale" v-if="this.finale == true" prepend-icon="mdi-trophy-outline"
      subtitle="Il tuo prodotto preferito...">
      <template v-slot:title>
        <span class="font-weight-black">Winner</span>
      </template>

      <v-card-text class="bg-surface-light">
        <v-row class="mb-10">
          <v-col>
            <v-card class="mx-auto" max-width="400" v-if="this.dx.length">
              <v-img class="align-end text-white" height="200" :src="this.getImage(this.dx[0].images[0])"
                cover>

                <!-- <v-img class="align-end text-white" height="200" :src="this.sx[this.p - 1].images[0]" cover> -->
                <v-card-title>{{ this.dx[0].title }}</v-card-title>
              </v-img>

              <v-card-subtitle class="pt-4">
                {{ this.dx[0].description }}
              </v-card-subtitle>

              <v-card-text>
                <div>
                  <v-list>
                    <v-list-subheader>Categoria</v-list-subheader>
                    <v-list-item :prepend-avatar="this.dx[0].category.image"
                      :title="this.dx[0].category.name">
                    </v-list-item>
                  </v-list>
                </div>
                <div>Prezzo: € {{ this.dx[0].price }}</div>
              </v-card-text>

              <v-card-actions>
                <v-btn color="orange" text="Nuovo" @click="this.new()"></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <v-dialog v-model="dialog" width="auto">
      <v-card max-width="400" prepend-icon="mdi-update" text="Preparati per il prossimo Round" title="Info">
        <v-sheet class="pa-4 text-center mx-auto" elevation="12" max-width="600" rounded="lg" width="100%">
          <v-icon class="mb-5" color="success" icon="mdi-check-circle" size="112"></v-icon>

          <h2 class="text-h5 mb-6">Round terminato!</h2>
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

    <v-dialog v-model="dialog2" width="auto">
      <v-card max-width="400" prepend-icon="mdi-trophy-outline" text="Prodotto più votato" title="Winner !!!">
        <v-sheet class="pa-4 text-center mx-auto" elevation="12" max-width="600" rounded="lg" width="100%">
          <v-icon class="mb-5" color="success" icon="mdi-trophy-outline" size="112"></v-icon>

          <h2 class="text-h5 mb-6">Votazione terminata!</h2>
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
      terzo: false,
      quarto: false,
      quinto: false,
      finale: false,
      dialog: false,
      dialog2: false,
      cambiato: false,
    }

  },
  methods: {
    async getProdotti() {
      await fetch('https://api.escuelajs.co/api/v1/products?offset=0&limit=32')
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
        this.cambiato = false;
        let numero = this.disponibili.length;
        console.log("numero: "+numero);
        if (numero == 0) {
          console.log('finiti i prodotti');
          if (this.primo == true && this.cambiato == false) {
            this.dialog = true;
            this.primo = false;
            this.secondo = true;
            this.cambiato = true;
          }
          if (this.secondo == true && this.cambiato == false) {
            this.dialog = true;
            this.secondo = false;
            this.terzo = true;
            this.cambiato = true;
          }
          if (this.terzo == true && this.cambiato == false) {
            this.dialog = true;
            this.terzo = false;
            this.quarto = true;
            this.cambiato = true;
          }
          if (this.quarto == true && this.cambiato == false) {
            this.dialog = true;
            this.quarto = false;
            this.quinto = true;
            this.cambiato = true;
          }
          if (this.quinto == true && this.cambiato == false) {
            // this.dialog = true;
            this.quinto = false;
            this.finale = true;
            this.cambiato = true;
          }
          if (this.finale == true && this.cambiato == false) {
            this.dialog2 = true;
          }

          //aspetta 1 secondo
          // setTimeout(() => {
          //   this.scrollSecondoSection();
          // }, 1000);
          this.reset();
        }
        if(this.finale == true){
          this.dx.push(this.disponibili[0]);

          let nuovoVincitore = this.dx[0];
          let vincitoriAttuali = JSON.parse(localStorage.getItem("winner")) || [];
          vincitoriAttuali.push(nuovoVincitore);
          localStorage.setItem("winner", JSON.stringify(vincitoriAttuali));
          this.dialog2 = true;
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
    },
    reset() {
      this.disponibili = [];
      this.estratti = [];
      this.voti.forEach(e => {
        this.disponibili.push(e);
      });
      console.log(this.disponibili.length);
      this.sx = [];
      this.dx = [];
      this.pos = 0;
      this.p = 0;
      this.voti = [];
      console.log('reset');
    },
    new() {
      location.reload();

      // this.disponibili = [];
      // this.prodotti.forEach(p => {
      //   this.disponibili.push(p);
      // });
      // this.estratti = [];
      // this.voti = [];
      // this.sx = [];
      // this.dx = [];
      // this.pos = 0;
      // this.p = 0;
      // this.estrai();
      // this.primo = true;
      // this.secondo = false;
      // this.terzo = false;
      // this.quarto = false;
      // this.quinto = false;
      // this.finale = false;
      // this.dialog = false;
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
