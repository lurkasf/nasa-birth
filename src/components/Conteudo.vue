<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-2">
        <h1 class="display-1 font-weight-medium mb-1">
          Descubra a foto que a NASA tirou no dia do seu nascimento
        </h1>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col
              cols="12"
              sm="6"
              md="4"
      >
        <v-dialog
                ref="dialog"
                v-model="modal"
                :return-value.sync="date"
                persistent
                width="290px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
                    v-model="date"
                    label="Selecione uma data"
                    prepend-icon="mdi-calendar"
                    readonly
                    v-bind="attrs"
                    v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker
                  v-model="date"
                  scrollable
                  locale="pt-br"
                  :max="new Date().toISOString().slice(0,10)"
          >
            <v-spacer></v-spacer>
            <v-btn
                    text
                    color="primary"
                    @click="modal = false"
            >
              Cancel
            </v-btn>
            <v-btn
                    text
                    color="primary"
                    @click="$refs.dialog.save(date)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-dialog>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-btn @click="abrirNasa()" color="indigo" class="white--text">
        CONFIRMAR
      </v-btn>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'Content',
    data: () => ({
      date: null,
      menu: false,
      modal: false,
      menu2: false,
    }),
    methods:{
      abrirNasa(){
        const codigo = this.date.replaceAll('-','').substring(2);
        const urlFinal = 'https://apod.nasa.gov/apod/ap' + codigo + '.html'
        window.open(urlFinal, "_blank", "");
      }
    }
  }
</script>
