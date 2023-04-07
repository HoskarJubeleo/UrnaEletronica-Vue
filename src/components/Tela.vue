<template>
    <div class="urna-tela">
        <div v-if="tela != 'fim'" class="urna-tela-voto">
            <div class="urna-tela-voto-textos">
                <div class="urna-tela-voto-titulo">Seu voto vai para: </div>
                <div class="urna-tela-voto-tipo">{{ tela }}</div>
                <div class="urna-tela-voto-numeros">
                    Numeros
                    <div class="urna-tela-voto-numero" v-for = "(value, key) in numeroVoto.padEnd(quantidadeNumeros,' ')" :key="key" >
                        {{ value }}
                    </div>
                </div>

                <div class="urna-tela-voto-descricao">
                    Nome: <strong> {{ candidato.nome ? candidato.nome : "  ____________" }} </strong>
                </div>

                <div class="urna-tela-voto-descricao">
                    Partido: <strong> {{ candidato.partido ? candidato.partido : "  ___________" }} </strong>
                </div>
            </div>
            <div v-if="candidato.imagem" class="urna-tela-voto-imagem">

                <img  :src="candidato.imagem"/>

            </div>
            <div class="urna-tela-voto-instrucoes">
                
                <p>Aperte as Telcas:</p>
                <p>BRANCO: Voto em Branco</p>
                <p>LARANJA: Corrigir</p>
                <p>VERDE: Confirmar</p>

            </div>
        </div>
        <div v-if="tela == 'fim'" class="urna-tela-fim">
            FIM!
        </div>
    </div>
</template>

<script>
export default {
    name: "Tela",
    props: {
        tela: String,
        numeroVoto: String,
        quantidadeNumeros: Number,
        candidato: Object
    }
}
</script>

<style>
    .urna-tela{
        width: 55%;
        height: 100%;
        padding: 1.1em;
        color: var(--dark-text-color);
        border: solid 2px var(--light-border-color);
        border-radius: 5px;
        background: var(--ballot-box-screen-color);
        box-shadow: var(--box-shadon);
    }

    .urna-tela-voto{
        width: 100%;
        height: 100%;
        display: flex;
        flex-wrap: wrap;
    }

    .urna-tela-voto-textos{
        flex: 1;
    }

    .urna-tela-voto-titulo{
        font-size: 1.3em;
    }

    .urna-tela-voto-tipo{
        margin: 1.1em 0;
        font-size: 1.5em;
        font-weight: bold;
        text-transform: uppercase;
    }

    .urna-tela-voto-numeros{
        display: flex;
        align-items: center;
    }

    .urna-tela-voto-numero{
        width: 45px;
        height: 55px;
        margin: 0 .2em;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.5em;
        font-weight: 500;
        border: solid 1px var(--dark-border-color);
        border-radius: 5px;
        box-shadow: 0 0 1px 1px rgba(0, 0, 0, .2);
    }

    .urna-tela-voto-descricao{
        margin: 1.2em 0;
    }

    .urna-tela-voto-imagem img{
        width: 110px;
        height: 150px;
        border: solid 1px var(--dark-border-color);
        border-radius: 5px;
        box-shadow: var(--box-shadon)
    }

    .urna-tela-voto-instrucoes{
        width: 100%;
        padding: 1em;
        border-top: solid 2px var(--dark-border-color);
        font-size: 1.1em;
    }

    .urna-tela-fim{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 5em;
        font-weight: bold;
    }
</style>