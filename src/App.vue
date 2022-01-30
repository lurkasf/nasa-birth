<template>
  <v-app>
    <v-app-bar app color="purple" dark>
      <div class="d-flex align-center">
        <a href="https://github.com/lurkasf" target="_blank" style="text-decoration: none">
          <v-icon>mdi-github</v-icon>
        </a>
      </div>

      <v-spacer></v-spacer>

      <v-btn v-if="exibirCopiar()" @click="compartilhar()" text>
        <span v-if="!exibirCopiado">
          <span class="mr-2">Compartilhar</span>
          <v-icon>mdi-share-variant</v-icon>
        </span>
        <span v-else>
          <span class="mr-2">Copiado</span>
          <v-icon>mdi-check-circle</v-icon>
        </span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Conteudo id="conteudo"/>
    </v-main>

  </v-app>
</template>

<script>
import Conteudo from './components/Conteudo';

export default {
  name: 'App',

  components: {
    Conteudo
  },
  data: () => ({
    showTooltip: false,
    exibirCopiado: false
  }),
  methods:{
    async compartilhar(){
      if(navigator.share){
        await navigator.share({
          title: document.title,
          text: 'Veja qual foto a NASA tirou no dia do seu nascimento!',
          url: window.location.href
        }).then(() => console.log('Compartilhado! 🎉')).catch(err => console.error(err));
      }else {
        const setExibir = (valor) => {
          this.exibirCopiado = valor
        }
        await navigator.clipboard.writeText(window.location.href);
        setExibir(true)
        setTimeout(function () {
          setExibir(false)
        }, 2500);
      }
    },
    exibirCopiar(){
      return false //TODO o botao nao funciona no in-app browser do instagram :(
    }
  }
};
</script>
<style>
</style>
