<template>
  <div class="urna-teclado">

    <div class="urna-teclado-numerico">
        <div class="urna-teclado-numerico-linha">
            <button v-on:click="adicionarNumero(1)">1</button>
            <button v-on:click="adicionarNumero(2)">2</button>
            <button v-on:click="adicionarNumero(3)">3</button>
        </div>
        <div class="urna-teclado-numerico-linha">
            <button v-on:click="adicionarNumero(4)">4</button>
            <button v-on:click="adicionarNumero(5)">5</button>
            <button v-on:click="adicionarNumero(6)">6</button>
        </div>
        <div class="urna-teclado-numerico-linha">
            <button v-on:click="adicionarNumero(7)">7</button>
            <button v-on:click="adicionarNumero(8)">8</button>
            <button v-on:click="adicionarNumero(9)">9</button>
        </div>
        <div class="urna-teclado-numerico-linha">
            <button v-on:click="adicionarNumero(0)">0</button>
        </div>
    </div>

    <div class="urna-teclado-acoes">
        <button class="btn-branco" v-on:click="votarBranco()">BRANCO</button>
        <button class="btn-corrige" v-on:click="corrigir()">CORRIGE</button>
        <button class="btn-confirma" v-on:click="confirmar()">CONFIRMA</button>
    </div>

  </div>
</template>

<script>
    export default {
        name: "Teclado",
        props: {
            adicionarNumero: Function,
            corrigir: Function,
            confirmar: Function,
            votarBranco: Function,
        }
    }
</script>

<style scoped>
    .urna-teclado{
        width: 40%;
        height: 100%;
        padding: 1.5em;
        border-radius: 5px;
        background: var(--ballot-box-keyboard-color);
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        box-shadow: 0 0 10px 1px rgba(0, 0, 0, .4);
    }

    .urna-teclado-numerico{
        width: 100%;
    }

    .urna-teclado-numerico-linha{
        display: flex;
        justify-content: space-around;
    }
    .urna-teclado-numerico button{
        margin: .8em 0;
        padding: .5em 1.5em;
        font-size: 1.1em;
        border-radius: 5px;
        background: var(--ballot-box-keyboard-button-color);
        color: var(--light-text-color);
    }

    .urna-teclado-acoes{
        width: 100%;
        display: flex;
        justify-content: space-between;
    }

    .urna-teclado-acoes button{
        width: 30%;
        height: 50px;
        padding: .5em;
        border-radius: 5px;
        font-size: 1em;
        color: var(--dark-text-color);
    }

    .btn-branco{
        background: var( --ballot-box-white-button-color);
    }
    .btn-corrige{
        background: var( --ballot-box-correct-button-color);
    }
    .btn-confirma{
        background: var( --ballot-box-confirm-button-color);
    }

</style>