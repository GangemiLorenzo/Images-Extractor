<template>
  <v-app>
    <v-toolbar fixed app>
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container>
        <v-slide-y-transition mode="out-in">
           <v-flex xs12>

            <v-card>
              <v-layout row>
                
                <v-flex xs5>
                  <v-img
                    :src="img_path"
                    height="250px"
                    contain
                  ></v-img>
                </v-flex>

                <v-flex xs7>
                  <v-card-title primary-title>
                    
                      <v-form v-if="show">
                        <v-layout row wrap>
                          <v-text-field
                            :value="img_dati[this.n].Nome"
                            readonly
                          ></v-text-field>
                          <v-text-field
                            :value="img_dati[this.n].Autore"
                            readonly
                          ></v-text-field>
                          <v-text-field
                            :value="img_dati[this.n].Luogo"
                            readonly
                          ></v-text-field>
                          <v-text-field
                            :value="img_dati[this.n].Data"
                            readonly
                          ></v-text-field>
                        </v-layout>
                      </v-form>
                      <v-form v-else>
                        <v-layout row wrap>
                          <v-text-field
                            readonly
                          ></v-text-field>
                          <v-text-field
                            readonly
                          ></v-text-field>
                          <v-text-field
                            readonly
                          ></v-text-field>
                          <v-text-field
                            readonly
                          ></v-text-field>
                        </v-layout>
                      </v-form>

                  </v-card-title>
                </v-flex>

              </v-layout>
              <v-btn
                v-if="!show"
                fab
                absolute
                bottom
                right
                @click="show = true"
              >
                <v-icon>spellcheck</v-icon>
              </v-btn>
              <v-btn
                v-if="show"
                fab
                absolute
                bottom
                right
                @click="next()"
              >
                <v-icon>navigate_next</v-icon>
              </v-btn>
            </v-card>

          </v-flex>
        </v-slide-y-transition>
      </v-container>
      <v-container>
        <v-flex>
          <div class="text-xs-center">
            <v-chip>{{counter}}</v-chip>
          </div>
        </v-flex>
      </v-container>
    </v-content>
    <v-footer fixed app>
      <v-spacer/>
      <span>&copy; 2018 - Lorenzo Gangemi</span>
      <v-spacer/>
    </v-footer>
  </v-app>
</template>

<script>
import dati from 'public/dati_foto.json'
  export default {
    data () {
      return {
        title: 'Img-extractor.js',
        n: 0,
        show: false,
        numeri: []
      }
    },
    created: function () {
    },
    methods: {
      next: function ()
      {
        this.show = false
        let numero = Math.floor(Math.random() * this.img_dati.length)
        if(this.numeri.indexOf(numero) === -1){
          this.n = numero
          this.numeri.push(numero)
        }
        else {
          if(this.numeri.length == this.img_dati.length) {
            alert("Ti sono state chieste tutte le immagini")
            this.numeri = []
          }
          this.next()
        }
      }
    },
    computed: {
      img_path: function() {
        return "/public/architettura/"+(this.n+1)+".png"
      },
      img_dati: function() {
        return dati
      },
      counter: function() {
        return this.numeri.length + "/" + this.img_dati.length
      }
    }
    
  }
</script>
