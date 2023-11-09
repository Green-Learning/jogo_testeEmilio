<template>
  <div class="lixeira" :class="tipoLixo"> 
    <img :src="getLixeiraImage(tipoLixo)" alt="Lixeira" class="imagem-lixeira"/>
  </div>
</template>

<script>
export default {
props: {
  tipoLixo: String, // Pode ser 'reciclável' ou 'orgânico'
},

methods: {
    getLixeiraImage(tipoLixo) {
      // Substitua os caminhos abaixo com os caminhos corretos para suas imagens de lixeira
      if (tipoLixo === 'reciclável') {
        return require('@/assets/lixeiras/blue.png');
      } else if (tipoLixo === 'orgânico') {
        return require('@/assets/lixeiras/brown.png');
      } else {
        // Defina um caminho de imagem padrão ou retorne null se não houver correspondência
        return null;
      }
    },
  },

};
</script>

<style scoped>
.lixeira {
width: 150px;
height: 200px;
display: flex;
align-items: center;
justify-content: center;
font-size: 18px;
cursor: pointer;
}

.imagem-lixeira {
  max-width: 100%; /* Para redimensionar a imagem */
  max-height: 100%; /* Para redimensionar a imagem */
}

.reciclável {

color: white;
}

.orgânico {

color: white;
}
</style>
