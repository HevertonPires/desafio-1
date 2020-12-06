# desafio-1
Primeiro desafio do <b>Curso JS</b> ministrado por [Heverton P. da Luz](https://www.linkedin.com/in/heverton-pires-da-luz/).

# Descrição do desafio

### 1. Criar um novo projeto utilizando vue-cli (vue create <nome_do_projeto>)

### 2. Sua pagida deve atender o seguinte requisito:
 1. Deve ser um jogo onde temos 2 personagens, 1 jogador e 1 mosntro, ambos começam com 100% de vida;

 2. Deve ter as opçoes para o jogador de atacar, ataque especial, curar e reiniciar a partida;

 3. Se o jogador chegar a 0% de vida o sistema deve apresentar <b>GAME OVER!</b>, caso o montro chegar a 0% deve apresentar <b>JOGADOR VENCEU!</b>

 4. O sistema deve listar cada passo, cada ataque e o quanto de dano cada jogador sofreu e o quanto ganhou de cura;

 5. O sistema deve exibir duas barras com a porcentagem de vida de cada jogador e quando a vida de algum dos jogadores atingir menos de 20% a barra de vida deve ficar na cor vermelha;

 6. O sistema deve ser componentizado, ou seja, tem que haver mais de um arquivo alem de App.vue;

### 3. As opções devem seguir as seguintes regras:
 1. Ataque: Deve gerar um valor aleatorio de até 10 e esse valor vai ser a força do ataque do monstro no jogador. A mesma função usada para calcular a força do ataque do mostro deve ser utilizada para calcular a força do ataque do jogador, porém, o valor aleatorio até 9. O valor calculado deve ser diminuido pelas vidas, jogador incide no mostro e vice-versa.

 2. Ataque especial: Ataque especial é um ataque, porém, com limites diferentes. Mostro com limite até 8 e jogador até 10.

 3. Cura: Deve gerar um valor de cura com limite de até 10, esse valor deve ser somado a vida do jogador. Lembrando que essa somada deve respeitar o limite de 100% de vida. Toda cura gera um ataque do monstro no jogador, onde o limite do ataque é 7.

 4. Reiniciar: Deve voltar a um estado iniciar com as vidas em 100%, ganhador restaurado e os logs limpos.
 
### 4. A função de geração de valores aleatorios é dada: 
  `
    gerarValorAleatorio (limite = 10) {
      return Math.floor(Math.random() * limite + 1)
    }
  `
