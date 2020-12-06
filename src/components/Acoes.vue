<template>
  <div class="painel h-100">
    <div>
      <button
        @click="atacar(10, 9)"
        class="botao bg-red"
      >ATACAR</button>
      <button
        @click="atacar(8, 10, true)"
        class="botao bg-yellow"
      >ATAQUE ESPECIAL</button>
      <button
        @click="curar"
        class="botao bg-orange"
      >CURAR</button>
      <button
        @click="iniciar"
        class="botao bg-grey"
      >REINICIAR</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    iniciar () {
      this.$emit('iniciar')
    },

    atacar (monstro, jogador) {
      this.$emit('atacar', { monstro, jogador })
    },

    curar () {
      this.$emit('curar')
      this.atacar(7, 0)
    }
  }
}
</script>