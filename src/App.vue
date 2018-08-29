<template>
  <v-app>
    <v-toolbar fixed app>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer/>
      <v-toolbar-items>
        <v-menu :close-on-content-click="false">
        <v-toolbar-title slot="activator">
          <span>Settori</span>
          <v-icon>arrow_drop_down</v-icon>
        </v-toolbar-title>

        <v-list>
         <v-list-tile>
            <v-list-tile-action v-if="bool_sedie || bool_design">
              <v-checkbox v-model="bool_architettura"></v-checkbox>
            </v-list-tile-action>
            <v-list-tile-content @click="bool_architettura = !bool_architettura">
              <v-list-tile-title>Architettura</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-action  v-if="bool_architettura || bool_design">
              <v-checkbox v-model="bool_sedie"></v-checkbox>
            </v-list-tile-action>
            <v-list-tile-content @click="bool_sedie = !bool_sedie">
              <v-list-tile-title>Arredamento</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-action  v-if="bool_sedie || bool_architettura">
              <v-checkbox v-model="bool_design"></v-checkbox>
            </v-list-tile-action>
            <v-list-tile-content @click="bool_design = !bool_design">
              <v-list-tile-title>Design</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-menu>
      </v-toolbar-items>
    </v-toolbar>
    <v-content>
      <v-container>
        <v-slide-y-transition mode="out-in">
           <v-flex xs12>

            <v-card>
              <v-layout row v-if="!$vuetify.breakpoint.xsOnly">
                
                <v-flex xs5>
                  <v-img
                    :src="img_path"
                    height="250px"
                    contain
                  ></v-img>
                </v-flex>

                <v-flex xs7>
                  <v-card-title primary-title>
                    
                      <v-form>
                        <v-layout row>
                          <v-flex ma-2>
                            <v-text-field v-if="lista[this.n].Autore"
                            label="Autore"
                            :disabled="!show"
                            :value="show? lista[this.n].Autore:''"
                            readonly
                          ></v-text-field>
                          <v-text-field v-if="lista[this.n].Luogo"
                            label="Luogo"
                            :disabled="!show"
                            :value="show? lista[this.n].Luogo:''"
                            readonly
                          ></v-text-field>
                          </v-flex>
                          <v-flex ma-2>
                          <v-text-field v-if="lista[this.n].Nome"
                            label="Nome"
                            :disabled="!show"
                            :value="show? lista[this.n].Nome:''"
                            readonly
                          ></v-text-field>
                          <v-text-field v-if="lista[this.n].Data"
                            label="Data"
                            :disabled="!show"
                            :value="show? lista[this.n].Data:''"
                            readonly
                          ></v-text-field>
                          </v-flex>
                        </v-layout>
                      </v-form>
                      
                  </v-card-title>
                </v-flex>

              </v-layout>
              <v-layout column v-else>

                <v-img
                  :src="img_path"
                ></v-img>

                <v-card-title primary-title>
                    <v-form>
                      <v-layout row>
                        <v-flex ma-2>
                            <v-text-field v-if="lista[this.n].Autore"
                            label="Autore"
                            :disabled="!show"
                            :value="show? lista[this.n].Autore:''"
                            readonly
                          ></v-text-field>
                          <v-text-field v-if="lista[this.n].Luogo"
                            label="Luogo"
                            :disabled="!show"
                            :value="show? lista[this.n].Luogo:''"
                            readonly
                          ></v-text-field>
                          </v-flex>
                          <v-flex ma-2>
                          <v-text-field v-if="lista[this.n].Nome"
                            label="Nome"
                            :disabled="!show"
                            :value="show? lista[this.n].Nome:''"
                            readonly
                          ></v-text-field>
                          <v-text-field v-if="lista[this.n].Data"
                            label="Data"
                            :disabled="!show"
                            :value="show? lista[this.n].Data:''"
                            readonly
                          ></v-text-field>
                          </v-flex>
                      </v-layout>
                    </v-form>
                </v-card-title>

              </v-layout>
              <v-btn 
                v-if="!show && !$vuetify.breakpoint.xsOnly"
                fab
                absolute
                bottom
                right
                @click="show = true"
              >
                <v-icon>spellcheck</v-icon>
              </v-btn>
              <v-btn
                v-if="show && !$vuetify.breakpoint.xsOnly"
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

    <v-btn 
      v-if="!show && $vuetify.breakpoint.xsOnly"
      fab
      fixed
      bottom
      right
      @click="show = true"
    >
      <v-icon>spellcheck</v-icon>
    </v-btn>
    <v-btn
      v-if="show && $vuetify.breakpoint.xsOnly"
      fab
      fixed
      bottom
      right
      @click="next()"
    >
      <v-icon>navigate_next</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
import architettura from 'public/architettura.json'
import sedie from 'public/sedie.json'
import design from 'public/design.json'
  export default {
    data () {
      return {
        title: 'Img-extractor.js',
        n: 0,
        show: false,
        numeri: [],
        bool_architettura: true,
        bool_sedie: true,
        bool_design: true
      }
    },
    created: function () {
    },
    methods: {
      next: function ()
      {
        this.show = false
        let numero = Math.floor(Math.random() * this.lista.length)
        if(this.numeri.indexOf(numero) === -1){
          this.n = numero
          this.numeri.push(numero)
        }
        else {
          if(this.numeri.length == this.lista.length) {
            alert("Ti sono state chieste tutte le immagini")
            this.numeri = []
          }
          this.next()
        }
      }
    },
    computed: {
      img_path: function() {
        return "/public/foto/"+this.lista[this.n].Immagine+".png"
      },
      architettura: function() {
        return architettura
      },
      sedie: function() {
        return sedie
      },
      design: function() {
        return design
      },
      lista: function() {
        let lst = []
        let architettura = this.architettura
        let sedie = this.sedie
        let design = this.design
        if(this.bool_architettura)
        architettura.forEach((a, i) => {
          lst.push(a);
        })
        if(this.bool_sedie)
        sedie.forEach((sedia, i) => {
          lst.push(sedia);
        })
        if(this.bool_design)
        design.forEach((d, i) => {
          lst.push(d);
        })
        this.numeri = []
        this.n = 0
        return lst
      },
      counter: function() {
        return this.numeri.length + "/" + this.lista.length
      }
    }
    
  }
</script>
