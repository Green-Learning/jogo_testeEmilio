<template>
  <div class="tela-jogo">
    <div class="pontuacao">Pontuação: {{ pontuacao }}</div>
    <Lixeira tipoLixo="reciclável" ref="lixoReciclavel" />
    <Lixeira tipoLixo="orgânico" ref="lixoOrganico" />
    
    <ItemLixo
      v-for="(item, index) in itens"
      :key="index"
      v-show="!item.removido"
      :tipoLixo="item.imageURL"
      :tiposLixeira="item.tiposLixeira"
      @itemDescartado="lidarItemDescartado(item, index)"
    />
    
    <div v-show="mostrarMensagemParabens">
      Parabéns! Todos os itens foram descartados corretamente!
    </div>
  </div>
</template>

<script>
import Lixeira from "@/components/TrashBin.vue";
import ItemLixo from "@/components/TrashItem.vue";

export default {
  components: {
    Lixeira,
    ItemLixo,
  },
  data() {
    return {
      itens: [
        { tipo: "garrafa", tiposLixeira: ["reciclável"], removido: false, imageURL: require('@/assets/lixos/reciclaveis/garrafa.png') },
        { tipo: "plástico", tiposLixeira: ["reciclável"], removido: false, imageURL: require('@/assets/lixos/reciclaveis/plastico.png') },
        { tipo: "copo", tiposLixeira: ["reciclável"], removido: false, imageURL: require('@/assets/lixos/reciclaveis/copo.png') },
        { tipo: "pizza", tiposLixeira: ["orgânico"], removido: false, imageURL: require('@/assets/lixos/organicos/pizza.png') },
        { tipo: "biscoito", tiposLixeira: ["orgânico"], removido: false, imageURL: require('@/assets/lixos/organicos/biscoito.png') },
        { tipo: "hambúrguer", tiposLixeira: ["orgânico"], removido: false, imageURL: require('@/assets/lixos/organicos/hamburguer.png') },
      ],
      pontuacao: 0,
    };
  },
  computed: {
    mostrarMensagemParabens() {
      return this.itens.every(item => item.removido);
    },
  },
  methods: {
    lidarItemDescartado(item, index) {
      const tipoLixeira = item.tiposLixeira[0];

      if (tipoLixeira === 'reciclável' && item.tiposLixeira.includes(tipoLixeira)) {
        this.pontuacao += 10;
        console.log(`Item '${item.tipo}' descartado na lixeira correta (${tipoLixeira}). Pontuação: ${this.pontuacao}`);
        this.itens[index].removido = true;
      } else if (tipoLixeira === 'orgânico' && item.tiposLixeira.includes(tipoLixeira)) {
        this.pontuacao += 10;
        console.log(`Item '${item.tipo}' descartado na lixeira correta (${tipoLixeira}). Pontuação: ${this.pontuacao}`);
        this.itens[index].removido = true;
      } else {
        console.log(`Item '${item.tipo}' descartado na lixeira errada (${tipoLixeira}). Pontuação: ${this.pontuacao}`);
      }

      if (this.mostrarMensagemParabens) {
        console.log('Parabéns! Todos os itens foram descartados corretamente!');
        // Aqui você pode adicionar outra ação, como exibir um modal ou realizar qualquer outra ação desejada
      }
    },

    handleLixoDescartadoNoLugarErrado(item) {
      const tipoLixeira = item.tiposLixeira[0];

      if (tipoLixeira === 'reciclável' && !item.tiposLixeira.includes(tipoLixeira)) {
        console.log(`Lixo '${item.tipo}' descartado na lixeira errada (${tipoLixeira}). Pontuação: ${this.pontuacao}`);
        // Adicione a ação específica se o lixo foi descartado na lixeira errada.
      } else if (tipoLixeira === 'orgânico' && !item.tiposLixeira.includes(tipoLixeira)) {
        console.log(`Lixo '${item.tipo}' descartado na lixeira errada (${tipoLixeira}). Pontuação: ${this.pontuacao}`);
        // Adicione a ação específica se o lixo foi descartado na lixeira errada.
      }
    },

  },
};
</script>

<style scoped>
.tela-jogo {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.pontuacao {
  font-size: 24px;
  margin-bottom: 20px;
}
</style>
