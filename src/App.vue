<template>
  <div>
    <div class="painel h-200">
      <div
        id="jogador"
        class="jogadores"
      >
        <p style="font-size: x-large;">Jogador</p>
        <div class="barra">
          <div
            class="preenchimento"
            :style="{width: `${vidaJogador}%`, 'background-color': corBarJ}"
          ></div>
        </div>
        <p>{{`${vidaJogador}%`}}</p>
      </div>
      <div
        id="monstro"
        class="jogadores"
      >
        <p style="font-size: x-large;">Monstro</p>
        <div class="barra">
          <div
            class="preenchimento"
            :style="{width: `${vidaMonstro}%`, 'background-color': corBarM}"
          ></div>
        </div>
        <p>{{`${vidaMonstro}%`}}</p>
      </div>
    </div>
    <div
      class="painel h-100 ganhador"
      v-if="ganhador"
      :style="{color: corGanhador}"
    >
      {{ganhador}}
    </div>
    <acoes
      ref="acoes"
      @iniciar="iniciar"
      @atacar="atacar"
      @curar="curar"
    ></acoes>
    <logs :logs="logs"></logs>
  </div>
</template>

<script>
import Acoes from './components/Acoes'
import Logs from './components/Logs'
export default {
  components: {
    Logs,
    Acoes,
  },
  data () {
    return {
      vidaMonstro: 100,
      vidaJogador: 100,
      logs: [],
      corBarM: 'green',
      corBarJ: 'green',
      ganhador: '',
      corGanhador: ''
    };
  },
  methods: {
    iniciar () {
      this.vidaMonstro = this.vidaJogador = 100
      this.corBarJ = this.corBarM = 'green'
      this.ganhador = ''
      this.logs = []
    },

    ataque (forcaAtaqueMonstro, forcaAtaqueJogador) {
      let ataqueM = this.gerarValorAleatorio(forcaAtaqueMonstro)
      let ataqueJ = this.gerarValorAleatorio(forcaAtaqueJogador)
      let vidaJ = parseInt(this.vidaJogador) - ataqueM
      let vidaM = parseInt(this.vidaMonstro) - ataqueJ
      this.corBarJ = vidaJ <= 20 ? 'red' : 'green'
      this.corBarM = vidaM <= 20 ? 'red' : 'green'
      if (this.vidaJogador !== 0 && this.vidaMonstro !== 0) {
        forcaAtaqueJogador !== 0
          ? this.logs.push(`<b>Monstro</b> sofreu um dano de <b>-${ataqueJ}%</b>`)
          : vidaM = this.vidaMonstro

        this.logs.push(`<b>Jogador</b> sofreu um dano de <b>-${ataqueM}%</b>`)

        return {
          jogador: vidaJ >= 0 ? vidaJ : 0,
          monstro: vidaM >= 0 ? vidaM : 0
        }
      }
      return {
        jogador: this.vidaJogador,
        monstro: this.vidaMonstro
      }
    },

    atacar ({ jogador, monstro }) {
      let ataque = this.ataque(monstro, jogador)
      this.vidaMonstro = ataque.monstro
      this.vidaJogador = ataque.jogador
    },

    curar () {
      if (parseInt(this.vidaJogador) < 100) {
        let vCura = this.gerarValorAleatorio(10)
        let somaVida = parseInt(this.vidaJogador) + vCura
        this.vidaJogador = somaVida > 100 ? 100 : somaVida
        this.logs.push(`<b>Jogador</b> recebeu uma cura de <b>+${vCura}%</b>`)
      }
    },

    gerarValorAleatorio (offsetVal = 10) {
      return Math.floor(Math.random() * offsetVal + 1)
    }
  },

  watch: {
    vidaMonstro (novo) {
      if (parseInt(novo) <= 0) {
        this.ganhador = 'Jogador venceu !!!'
        this.corGanhador = 'green'
        this.$refs.acoes.reiniciar()
      }
    },
    vidaJogador (novo) {
      if (parseInt(novo) <= 0) {
        this.ganhador = 'Game Over !!!'
        this.corGanhador = 'red'
        this.$refs.acoes.reiniciar()
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.painel {
  display: flex;
  background-color: rgb(49, 48, 48);
  margin: 10px;
  box-shadow: 6px 6px 6px #4c00ff6d;
  text-align: center;
  justify-content: space-around;
  align-items: center;
}

.h-50 {
  height: 50px;
}

.h-100 {
  height: 100px;
}

.h-200 {
  height: 200px;
}

.h-auto {
  height: auto;
}

.jogadores {
  color: #fff;
  width: 40%;
  margin: 5px 20px 5px 20px;
  align-items: center;
}

.preenchimento {
  height: 100%;
}

.barra {
  width: 100%;
  height: 20px;
  background-color: #fff;
}

.botao {
  padding: 10px;
  font-size: smaller;
  border-radius: 5px;
  font-weight: bold;
  margin: 2px;
}

.bg-blue {
  background-color: blue;
  color: #fff;
}

.bg-yellow {
  background-color: yellow;
  color: #000;
}

.bg-red {
  background-color: red;
  color: #fff;
}

.bg-grey {
  background-color: grey;
  color: #000;
}

.bg-orange {
  background-color: orange;
  color: #000;
}

.ganhador {
  font-size: xx-large;
  font-weight: bold;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}
</style>
