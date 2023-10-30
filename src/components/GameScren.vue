<template>
    <div class="game-screen">
      <div class="score">Score: {{ score }}</div>
      <TrashBin binType="recyclable" />
      <TrashBin binType="organic" />
      
      <TrashItem
        v-for="(item, index) in items"
        :key="index"
        :itemType="item.type"
        :binTypes="item.binTypes"
        @itemDropped="handleItemDropped"
      />
    </div>
  </template>
  
  <script>
  import TrashBin from "@/components/TrashBin.vue";
  import TrashItem from "@/components/TrashItem.vue";
  
  export default {
    components: {
      TrashBin,
      TrashItem,
    },
    data() {
      return {
        items: [
          { type: "bottle", binTypes: ["recyclable"] },
          { type: "plastic", binTypes: ["recyclable"] },
          { type: "cup", binTypes: ["recyclable"] },
          { type: "pizza", binTypes: ["organic"] },
          { type: "cookie", binTypes: ["organic"] },
          { type: "burger", binTypes: ["organic"] },
        ],
        score: 0,
      };
    },
    methods: {
      handleItemDropped(itemType) {
        // Verifica se o itemType está na lista de binTypes da lixeira correta
        const item = this.items.find(item => item.type === itemType);
        console.log(item.binTypes);
        console.log(item.type);
        console.log(itemType);
        console.log(item);
        if (item && item.binTypes.includes(itemType)) {
          this.score += 10; // Incrementa a pontuação em 10
          console.log(`Item "${itemType}" dropped in the correct bin. Score: ${this.score}`);
        } else {
          console.log(`Item "${itemType}" dropped in the wrong bin. Score: ${this.score}`);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .game-screen {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
  }
  
  .score {
    font-size: 24px;
    margin-bottom: 20px;
  }
  </style>
  