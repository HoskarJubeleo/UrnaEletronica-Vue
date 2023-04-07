<template>
  <main id="app">
    <div id="urna">
      <Tela :tela="tela" :numeroVoto="numeroVoto" :quantidadeNumeros="quantidadeNumeros" :candidato="candidato"/> 
      <Teclado :adicionarNumero="adicionarNumero" :corrigir="corrigir" :confirmar="confirmar" :votarBranco="votarBranco"/>
  </div>

  <div id="tela-em-producao">
    <div class="box-producao">
      <img class="cell-img" src="https://cdn-icons-png.flaticon.com/512/33/33299.png">
      <img class="tablet-img" src="https://cdn-icons-png.flaticon.com/512/5699/5699678.png">

      <p class="cell-text">DESCULPE</p>
      <p class="cell-text">Não disponivel para celular no momento...</p>
      <p class="tablet-text">Gire a tela por favor</p>
    </div>
  </div>

  </main>
</template>

<script >

  import Teclado from './components/Teclado.vue';
  import Tela from './components/Tela.vue';

  import ConfirmAudio from './assets/audio/confirm.wav'
  import KeyAudio from './assets/audio/key.wav'

  export default {
    name: "App",
    components: {
      Teclado,
      Tela,
      
    },
    methods: {
      adicionarNumero(numero){
        //Executar SOM clcik teclas
        this.executarSom(KeyAudio); 

        //Manipular numeros -> Tela.vue
        //Vefirica Limite numero adicionados
        if(this.numeroVoto.length == this.quantidadeNumeros){
          return false;
        }

        //ADD numeros selecionados
        this.numeroVoto += '' + numero;

        //Verificar os Candidatos votados
        this.verificarCandidato();
      },
      verificarCandidato(){
        //Voto Incompleto
        if(this.numeroVoto.length < this.quantidadeNumeros){
          return false;
        }

        //Candidato Existente
        if(this.candidatos[this.tela][this.numeroVoto]){
          this.candidato = this.candidatos[this.tela][this.numeroVoto];
          return true;
        }

        //Voto Nulo
        this.candidato = {
          nome: "Voto NULO",
          partido: "Voto NULO",
          imagem: "",
        }
      },
      corrigir(){
        //Executar Som da tecla
        this.executarSom(KeyAudio);
        this.limpar();
      },
      limpar(){
        this.candidato = {}
        this.numeroVoto = '';
      },
      confirmar(){
        if(this.numeroVoto.length < this.quantidadeNumeros){
          return false;
        }

        return this.avancarTela();
      },
      avancarTela(){
        //Executar SOM confirmar
        this.executarSom(ConfirmAudio); 

        //Tela Vereador
        if(this.tela == 'prefeito'){
          this.tela = 'vereador';
          this.quantidadeNumeros = 5;
          return this.limpar();
        }
        //Tela Final
        this.tela = 'fim';

        //Instancia Atual
        var instancia = this;

        //Voltar ao inicio
        setTimeout(function(){
          instancia.tela = 'prefeito';
          instancia.quantidadeNumeros = 2;
          return instancia.limpar()
        },3000)
      },
      votarBranco(){
        if(this.tela == 'fim') return false;
        this.limpar();
        this.avancarTela();
      },
      executarSom(arquivoSom){
        if(arquivoSom){
          let audio = new Audio(arquivoSom);
          audio.play();
        }
      }
    },
    data() {
      return {
        tela: "prefeito",
        numeroVoto: '',
        quantidadeNumeros: 2,
        candidato: { },
        candidatos:{
          "prefeito":{
            "01":{
              "nome": "Ash",
              "partido": "Pokemon",
              "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/ash.png"
            },
            "08":{
              "nome": "Vegeta",
              "partido": "Dragon Ball",
              "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png"
            }
          },
          "vereador":{
            "01234":{
              "nome": "Pikachu",
              "partido": "Pokemon",
              "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/pikachu.png"
            },
            "08001":{
              "nome": "Goku",
              "partido": "Dragon Ball",
              "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/goku.png"
            }
          }        
        }
      }
    }
  }
  
</script>

<style>
  #app{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: var(--background-body);
  }

  #urna{
  width: 1000px;
  height: 500px;
  padding: 1.5em;
  display: flex;
  justify-content: space-between;
  border-radius: 5px;
  box-shadow: var(--box-shadon);
  background: var(--box-urna); 
}

#tela-em-producao{
  width: 100vw;
  height: 100vh;
  display: none;
}

.box-producao{
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 1em;
  overflow: hidden;
}

.cell-img, .tablet-img{
    width: 300px;
    margin: 1em 0 1em 0;
  }

  .cell-text, .tablet-text{
    font-size: 2em;
    font-weight: 600;
    color: var(--light-text-color);
    padding: 0 1em;
    text-align: center;
  }

@media (max-width: 480px){
  #urna{
    display: none;
  }

  #tela-em-producao{
    display: block;
  }

  .tablet-img, .tablet-text{
    display: none;
  }
}

@media (min-width: 600px){
  #urna{
    display: none;
  }

  #tela-em-producao{
    display: block;
  }

  .tablet-img, .tablet-text{
    display: block;
  }

  .cell-img, .cell-text{
    display: none;
  }
}

@media (min-width: 1024px){
  #urna{
    display: flex;
  }

  #tela-em-producao{
    display: none;
  }
}
</style>
